FROM debian
LABEL vendor="Ecole 42" \
			  com.tonio.version="0.0.1-beta" \
			  com.tonio.release-date="2017-05-16"


ENV TS_DIRECTORY=/opt/teamspeak


RUN apt-get update && apt-get install -y bzip2 w3m wget && rm -rf /var/lib/apt/lists/* &&\
  TS_SERVER_VER="$(w3m -dump https://www.teamspeak.com/downloads | grep -m 1 'Server 64-bit ' | awk '{print $NF}')" &&\
  wget http://dl.4players.de/ts/releases/${TS_SERVER_VER}/teamspeak3-server_linux_amd64-${TS_SERVER_VER}.tar.bz2 -O /tmp/teamspeak.tar.bz2 &&\
  tar jxf /tmp/teamspeak.tar.bz2 -C /opt &&\
  mv /opt/teamspeak3-server_* ${TS_DIRECTORY} &&\
  rm /tmp/teamspeak.tar.bz2 &&\
#  apt-get purge -y bzip2 w3m wget &&\
#  apt-get autoremove -y &&\
  rm -rf /var/lib/apt/lists/*


RUN groupadd -g 503 teamspeak &&\
  useradd -u 503 -g 503 -d ${TS_DIRECTORY} teamspeak &&\
  mkdir /data &&\
  chown -R teamspeak:teamspeak ${TS_DIRECTORY} /data


USER teamspeak
EXPOSE 9987/udp 10011 30033
WORKDIR $TS_DIRECTORY
ENTRYPOINT ["./ts3server_minimal_runscript.sh", "createinifile=1"]
# ENTRYPOINT ["./ts3server_startscript.sh", "start"]
