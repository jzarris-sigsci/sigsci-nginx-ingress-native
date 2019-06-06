FROM quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.22.0
USER root
# Pull the nginx version for the ingress controller
# Pull the latest module version from https://dl.signalsciences.net/sigsci-module-nginx-native/VERSION)
# Then pull the filename with the latest module version build number by listing https://dl-signalsciences-net.s3-us-west-2.amazonaws.com/?delimiter=/&prefix=sigsci-module-nginx-native/$SIGSCI_MODULE_VERSION/debian/stretch/
# Feed this into curl -O "https://dl.signalsciences.net/sigsci-module-nginx-native/$SIGSCI_MODULE_VERSION/debian/stretch/$SIGSCI_MODULE_BUILD"
# Then install $SIGSCI_MODULE_BUILD
RUN NGINX_BUILD=$(nginx -v 2>&1 | grep  -Po '(?<=nginx\/)[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}') ;\
  echo $NGINX_BUILD ;\
  SIGSCI_MODULE_VERSION=$(curl -sL https://dl.signalsciences.net/sigsci-module-nginx-native/VERSION) ; \
  SIGSCI_MODULE_BUILD=$(curl "https://dl-signalsciences-net.s3-us-west-2.amazonaws.com/?delimiter=/&prefix=sigsci-module-nginx-native/$SIGSCI_MODULE_VERSION/debian/stretch/" | grep -o 'nginx-module-sigsci-nxo_[^-]*-[^-]*-stretch_amd64.deb' | grep "$NGINX_BUILD") ; \
  echo $SIGSCI_MODULE_BUILD ; \
  curl -O "https://dl.signalsciences.net/sigsci-module-nginx-native/$SIGSCI_MODULE_VERSION/debian/stretch/$SIGSCI_MODULE_BUILD" ; \
  dpkg --force-all -i ./$SIGSCI_MODULE_BUILD
USER www-data
