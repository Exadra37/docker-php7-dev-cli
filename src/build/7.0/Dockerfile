FROM exadra37/php7-fpm:7.0

ARG CONTAINER_USER=php-fpm
ARG OH_MY_ZSH_THEME=bira

USER root

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install \
        nano \
        vim \
        curl \
        git \
        mysql-client \
        zsh && \

    # Install Composer
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    rm -rvf composer-setup.php && \

    # Install Oh My Zsh for root user
    bash -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \

    # Install Oh My Zsh for home user
    # change from /usr/sbin/nologin to /usr/sbin/zsh
    usermod -s /usr/bin/zsh "${CONTAINER_USER}" && \
    su "${CONTAINER_USER}" -c 'bash -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"' && \
    sed -i s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"${OH_MY_ZSH_THEME}\"/g /home/${CONTAINER_USER}/.zshrc

USER "${CONTAINER_USER}"

CMD ["zsh"]
