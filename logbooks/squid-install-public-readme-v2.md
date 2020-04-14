## ###################################################
## INSTALAÇÃO PROXY SQUID
## SCRIPT: v1 - Data: 22/03/2020 - 03:50 | TZ -3 BRT
## SCRIPT: v2 - Data: 22/03/2020 - 19:30 | TZ -3 BRT
## Descrição: Configuração pública
## Author: João Gerardo
## Contato: joaogerardo@gmail.com
## Fone: 47 9 8435-4307 - Whatsapp/Telegram/Fone
## ###################################################
## START) Considerações iniciais

Host: covid-chagas.vps.etica.ai / vps20038.publiccloud.com.br (191.252.103.250)

## ###################################################
## 1) instalação squid
sudo apt-get update && install squid

## ###################################################
## 2) configuração squid

# backup do arquivo de configuraçã original
cp -rp /etc/squid/squid.conf /etc/squid/squid.conf-orig

# sobrescreve a config configurar com os parâmetros
echo 'acl SSL_ports port 443
acl Safe_ports port 80		# http
acl Safe_ports port 21		# ftp
acl Safe_ports port 443		# https
acl Safe_ports port 70		# gopher
acl Safe_ports port 210		# wais
acl Safe_ports port 1025-65535	# unregistered ports
acl Safe_ports port 280		# http-mgmt
acl Safe_ports port 488		# gss-http
acl Safe_ports port 591		# filemaker
acl Safe_ports port 777		# multiling http
acl CONNECT method CONNECT
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost manager
http_access deny manager
http_access allow localhost
http_port 0.0.0.0:80
access_log daemon:/var/log/squid/access.log squid
coredump_dir /var/spool/squid
refresh_pattern ^ftp:		1440	20%	10080
refresh_pattern ^gopher:	1440	0%	1440
refresh_pattern -i (/cgi-bin/|\?) 0	0%	0
refresh_pattern (Release|Packages(.gz)*)$      0       20%     2880
refresh_pattern .		0	20%	4320
visible_hostname covid-chagas.vps.etica.ai
# o programa deve ser verificado o caminho correto
# depende da versao do squid
auth_param basic program /usr/lib/squid3/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Covid-Chagas Proxy Authentication
auth_param basic credentialsttl 2 hours
acl auth_users proxy_auth REQUIRED
http_access allow auth_users
http_access deny all
http_reply_access allow all
icp_access allow all
miss_access allow all' > /etc/squid/squid.conf

## ###################################################
## 3) instalação de integração de usuários
sudo apt-get install apache2-utils
sudo touch /etc/squid/passwd
sudo chown proxy: /etc/squid/passwd

## ###################################################
## 4) criação de usuários

# criação usuário
# podendo ser integrado via script com NGINX ou puxar
# de uma tabela ou lista de usuários e senhas.
#               script        usuario  senha
# Exemplo: $scriptPath.sh     john     nhoj

# recebe $1 e $2 e atribui à criação da conta
usuario=$1
senha=$2

sudo htpasswd -b /etc/squid/passwd $usuario $senha

## ###################################################
## 5) configurações finais da aplicação

# habilita o serviço para o startup
sudo systemctl enable squid

# inicia o serviço
sudo systemctl start squid

# reinicia o serviço
sudo systemctl start squid

# status do serviço
sudo systemctl status squid

## ###################################################
## 6) instruções de uso

curl -x "http://$usuario:$senha@covid-chagas.vps.etica.ai:80" https://ipinfo.io
{
  "ip": "191.252.103.250",
  "hostname": "vps18059.publiccloud.com.br",
  "city": "São Paulo",
  "region": "São Paulo",
  "country": "BR",
  "loc": "-23.5475,-46.6361",
  "org": "AS27715 Locaweb Serviços de Internet S/A",
  "postal": "01000-000",
  "timezone": "America/Sao_Paulo",
  "readme": "https://ipinfo.io/missingauth"
}

curl -s -x 'http://grodriguez:Covid-19-xG@covid-chagas.vps.etica.ai:80' http://cnes2.datasus.gov.br/Mod_Ind_Tipo_Leito.asp?VEstado=00 | html2text

CnesWeb - Cadastro Nacional de Estabelecimentos de Saúde
[imagem do topo cnes]


Indicadores - Cnes
                                   Consulta
                                    Leitos
Estado:
[One of: ESCOLHA ESTADO/Escolha/ACRE/ALAGOAS/AMAZONAS/AMAPA/BAHIA/CEARA/
DISTRITO FEDERAL/ESPIRITO SANTO/GOIAS/MARANHAO/MINAS GERAIS/MATO GROSSO DO
SUL/MATO GROSSO/PARA/PARAIBA/PERNAMBUCO/PIAUI/PARANA/RIO DE JANEIRO/RIO GRANDE
DO NORTE/RONDONIA/RORAIMA/RIO GRANDE DO SUL/SANTA CATARINA/SERGIPE/SAO PAULO/
TOCANTINS]
Município:                                                 [img/imprimir.gif]
[One of: ---MUNICÍPIO---]
Competência:
[One of: ---COMPETÊNCIA---]
 _____________________________________________________________________________
|Codigo|__________________________Descrição________|Existente|__Sus_|Não_Su|
|CIRÚRGICO____________________________________________________|
|___01_|BUCO_MAXILO_FACIAL___________________________|_____1119|___679|____440|
|___02_|CARDIOLOGIA__________________________________|_____5027|__2992|___2035|
|___03_|CIRURGIA_GERAL_______________________________|____58222|_37344|__20878|
|___04_|ENDOCRINOLOGIA_______________________________|______384|___125|____259|
|___05_|GASTROENTEROLOGIA____________________________|_____1894|___804|___1090|
|___06_|GINECOLOGIA__________________________________|_____6912|__4219|___2693|
|___08_|NEFROLOGIAUROLOGIA___________________________|_____3211|__1767|___1444|
|___09_|NEUROCIRURGIA________________________________|_____4860|__3508|___1352|
|___11_|OFTALMOLOGIA_________________________________|_____2481|__1151|___1330|
|___12_|ONCOLOGIA____________________________________|_____5078|__3490|___1588|
|___13_|ORTOPEDIATRAUMATOLOGIA_______________________|____18555|_14248|___4307|
|___14_|OTORRINOLARINGOLOGIA_________________________|_____2050|___737|___1313|
|___15_|PLASTICA_____________________________________|_____2560|___999|___1561|
|___16_|TORACICA_____________________________________|_____1088|___581|____507|
|___67_|TRANSPLANTE__________________________________|_____1274|__1034|____240|
|___90_|QUEIMADO_ADULTO______________________________|______233|___221|_____12|
|___91_|QUEIMADO_PEDIATRICO__________________________|_______88|____78|_____10|
|TOTAL_______________________________________________|___115036|_73977|__41059|

## ###################################################
## END) configurações compiladas no Proxy Squid

Squid Cache: Version 3.5.27
Service Name: squid
Ubuntu linux
configure options:  '--build=x86_64-linux-gnu' '--prefix=/usr' '--includedir=${prefix}/include' '--mandir=${prefix}/share/man' '--infodir=${prefix}/share/info' '--sysconfdir=/etc' '--localstatedir=/var' '--libexecdir=${prefix}/lib/squid3' '--srcdir=.' '--disable-maintainer-mode' '--disable-dependency-tracking' '--disable-silent-rules' 'BUILDCXXFLAGS=-g -O2 -fdebug-prefix-map=/build/squid3-a0_cdd/squid3-3.5.27=. -fstack-protector-strong -Wformat -Werror=format-security -Wno-error=deprecated -Wno-error=format-truncation -Wdate-time -D_FORTIFY_SOURCE=2 -Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -Wl,--as-needed' '--datadir=/usr/share/squid' '--sysconfdir=/etc/squid' '--libexecdir=/usr/lib/squid' '--mandir=/usr/share/man' '--enable-inline' '--disable-arch-native' '--enable-async-io=8' '--enable-storeio=ufs,aufs,diskd,rock' '--enable-removal-policies=lru,heap' '--enable-delay-pools' '--enable-cache-digests' '--enable-icap-client' '--enable-follow-x-forwarded-for' '--enable-auth-basic=DB,fake,getpwnam,LDAP,NCSA,NIS,PAM,POP3,RADIUS,SASL,SMB' '--enable-auth-digest=file,LDAP' '--enable-auth-negotiate=kerberos,wrapper' '--enable-auth-ntlm=fake,smb_lm' '--enable-external-acl-helpers=file_userip,kerberos_ldap_group,LDAP_group,session,SQL_session,time_quota,unix_group,wbinfo_group' '--enable-url-rewrite-helpers=fake' '--enable-eui' '--enable-esi' '--enable-icmp' '--enable-zph-qos' '--enable-ecap' '--disable-translation' '--with-swapdir=/var/spool/squid' '--with-logdir=/var/log/squid' '--with-pidfile=/var/run/squid.pid' '--with-filedescriptors=65536' '--with-large-files' '--with-default-user=proxy' '--enable-build-info=Ubuntu linux' '--enable-linux-netfilter' 'build_alias=x86_64-linux-gnu' 'CFLAGS=-g -O2 -fdebug-prefix-map=/build/squid3-a0_cdd/squid3-3.5.27=. -fstack-protector-strong -Wformat -Werror=format-security -Wall' 'LDFLAGS=-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -Wl,--as-needed' 'CPPFLAGS=-Wdate-time -D_FORTIFY_SOURCE=2' 'CXXFLAGS=-g -O2 -fdebug-prefix-map=/build/squid3-a0_cdd/squid3-3.5.27=. -fstack-protector-strong -Wformat -Werror=format-security -Wno-error=deprecated -Wno-error=format-truncation'

## configuração final squid  /etc/squid/squid.conf
acl SSL_ports port 443
acl Safe_ports port 80		# http
acl Safe_ports port 21		# ftp
acl Safe_ports port 443		# https
acl Safe_ports port 70		# gopher
acl Safe_ports port 210		# wais
acl Safe_ports port 1025-65535	# unregistered ports
acl Safe_ports port 280		# http-mgmt
acl Safe_ports port 488		# gss-http
acl Safe_ports port 591		# filemaker
acl Safe_ports port 777		# multiling http
acl CONNECT method CONNECT
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost manager
http_access deny manager
http_access allow localhost
http_port 0.0.0.0:80
access_log daemon:/var/log/squid/access.log squid
coredump_dir /var/spool/squid
refresh_pattern ^ftp:		1440	20%	10080
refresh_pattern ^gopher:	1440	0%	1440
refresh_pattern -i (/cgi-bin/|\?) 0	0%	0
refresh_pattern (Release|Packages(.gz)*)$      0       20%     2880
refresh_pattern .		0	20%	4320
visible_hostname covid-chagas.vps.etica.ai
# o programa deve ser verificado o caminho correto
# depende da versao do squid
auth_param basic program /usr/lib/squid3/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Covid-Chagas Proxy Authentication
auth_param basic credentialsttl 2 hours
acl auth_users proxy_auth REQUIRED
http_access allow auth_users
http_access deny all
http_reply_access allow all
icp_access allow all
miss_access allow all

## ###################################################
