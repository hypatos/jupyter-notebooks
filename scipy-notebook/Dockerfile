FROM quay.io/jupyteronopenshift/s2i-minimal-notebook-py36:2.5.1

USER root

COPY . /tmp/src

RUN rm -rf /tmp/src/.git* && \
    chown -R 1001 /tmp/src && \
    chgrp -R 0 /tmp/src && \
    chmod -R g+w /tmp/src && \
    rm -rf /tmp/scripts && \
    mv /tmp/src/.s2i/bin /tmp/scripts

ENV XDG_CACHE_HOME=/opt/app-root/src/.cache

RUN yum install -y unzip poppler-utils system-logos
RUN yum install -y https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/c/cabextract-1.5-1.el7.x86_64.rpm
RUN yum install -y curl xorg-x11-font-utils fontconfig cabextract
RUN yum install -y https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm

USER 1001

RUN /tmp/scripts/assemble

RUN pip install --upgrade pip
RUN pip install hycli
RUN pip install wand==0.5.8
RUN pip install pdf2image==1.12.1
RUN pip install PyPDF2

CMD [ "/opt/app-root/builder/run" ]
