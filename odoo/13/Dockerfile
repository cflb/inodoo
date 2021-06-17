FROM odoo:13.0
USER root
RUN mkdir /opt/odoo-install
COPY ./iugu-python /opt/odoo-install/iugu/
ADD odoo.conf /opt/odoo-install
WORKDIR /opt/odoo-install

RUN apt-get update
RUN apt-get install git -y
RUN apt-get install  build-essential python3.7-dev xmlsec1 libxmlsec1-dev libxmlsec1 pkg-config openssl python-lxml libxml2-dev libxmlsec1-openssl -y

WORKDIR /opt/odoo-install/iugu
RUN find /usr -name '*.pyc' -delete
RUN python3 setup.py install
RUN pip3 install mercadopago==1.1.1
WORKDIR /opt/odoo-install
#RUN pip3 install --user -U libsass --no-warn-script-location
#RUN python3 -m pip install -r pip-requirements
#USER root

USER odoo
RUN pip3 install --upgrade pip setuptools wheel

COPY ./odoo-brasil /mnt/extra-addons

RUN chown odoo:odoo /mnt/extra-addons

USER root
RUN chmod 775 -R /mnt/extra-addons

USER odoo
#WORKDIR /mnt/extra-addons
# Dependencias extra
RUN pip3 install xmlsec --trusted-host --extra-index-url=https://hoefling.io/pypi/
#RUN pip3 install -r requirements.txt

WORKDIR /opt/odoo-install

USER root
COPY ./odoo.conf /etc/odoo/odoo.conf
EXPOSE 8069