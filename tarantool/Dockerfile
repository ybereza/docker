FROM tarantool/tarantool:2.6.0
COPY config/tarantool/rootfs/etc/tarantool/instances.available/profiles-master.lua /etc/tarantool/instances.available/
RUN  mkdir -p /etc/tarantool/instances.enabled/ /var/log/tarantool /var/run/tarantool/ /opt/tarantool/data/ /opt/tarantool/data/profiles-master/ /opt/tarantool/data/wal/ /opt/tarantool/data/snaps/ /var/lib/tarantool/profiles-master/
RUN  mkdir -p /opt/WWWRoot/mrgservice/lua/profiles-master
RUN  chown -R tarantool:tarantool /var/log/tarantool
RUN  chown -R tarantool:tarantool /opt/tarantool
RUN  chown -R tarantool:tarantool /var/lib/tarantool
RUN  chown -R tarantool:tarantool /opt/WWWRoot
RUN  ln -s /etc/tarantool/instances.available/profiles-master.lua /etc/tarantool/instances.enabled/

ENTRYPOINT ["tarantool", "/etc/tarantool/instances.enabled/profiles-master.lua"]

HEALTHCHECK CMD tarantool_is_up

EXPOSE 3301
CMD ["tarantool"]
