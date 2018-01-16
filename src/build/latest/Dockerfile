FROM exadra37/php7-fpm:dev-7.2

ARG CONTAINER_USER='php-fpm'
ARG OH_MY_ZSH_THEME=${OH_MY_ZSH_THEME:-agnoster}
#ARG OH_MY_ZSH_THEME_PATH=${OH_MY_ZSH_THEME_PATH:-/home/${CONTAINER_USER}/.oh-my-zsh/themes}
#ARG OH_MY_ZSH_THEME_FILE=${OH_MY_ZSH_THEME_PATH}/${OH_MY_ZSH_THEME}.zsh-theme


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

    # Intall Oh My Zsh for root user
    bash -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \

    # Intall Oh My Zsh for root user
    # change from /usr/sbin/nologin to /usr/sbin/zsh
    usermod -s /usr/bin/zsh "${CONTAINER_USER}" && \
    su "${CONTAINER_USER}" -c 'bash -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"' && \
    #su "${CONTAINER_USER}" -c 'bash -c "$(mkdir -p ${OH_MY_ZSH_THEME_PATH})"' && \
    #su "${CONTAINER_USER}" -c 'bash -c "$(git clone https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme.git  ${OH_MY_ZSH_THEME_PATH})"' && \

    sed -i s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"${OH_MY_ZSH_THEME}\"/g /home/${CONTAINER_USER}/.zshrc


USER "${CONTAINER_USER}"

CMD ["zsh"]

