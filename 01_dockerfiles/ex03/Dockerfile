FROM ubuntu:16.04

MAINTAINER Aslan MALSAGOV <amalsago@student.42.fr>

RUN apt-get update \
	&& apt-get -y upgrade \
    && apt-get install -y --no-install-recommends \
					vim \
					curl \
					tzdata \
					postfix \
					openssh-server \
					ca-certificates

RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash \
	&& apt-get install -y --no-install-recommends gitlab-ce

RUN apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

RUN mkdir -p /etc/gitlab/ssl \
	&& chmod 700 /etc/gitlab/ssl \
	&& openssl req \
			-x509 \
			-days 365 \
			-newkey rsa:2048 -nodes \
			-keyout /etc/gitlab/ssl/aslan.gitlab.key \
			-out /etc/gitlab/ssl/aslan.gitlab.crt \
			-subj "/C=FR/ST=IDF/L=Paris/O=42/CN=www.aslan.gitlab.com"

RUN echo "external_url \"https://aslan.gitlab.com\"" >> /etc/gitlab/gitlab.rb \
	&& echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb \
	&& echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/aslan.gitlab.crt\"" >> /etc/gitlab/gitlab.rb \
	&& echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/aslan.gitlab.key\"" >> /etc/gitlab/gitlab.rb

EXPOSE 22 80 443

CMD (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && gitlab-ctl tail
