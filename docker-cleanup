#!/bin/bash
#
# Removes docker residue which can quickly consume massive amounts of disk space.
#
# See http://blog.yohanliyanage.com/2015/05/docker-clean-up-after-yourself/.
#
if [ ! $(command -v docker) ]; then
  echo "Docker is not installed."
  exit 1
fi
docker volume rm $(docker volume ls -qf dangling=true) 2> /dev/null
docker rmi $(docker images -f "dangling=true" -q) 2> /dev/null
VERSION=$(docker --version | cut -d' ' -f3 | cut -d',' -f1)
if [ $VERSION > 1.9 ]; then
  docker volume rm $(docker volume ls -qf dangling=true) 2> /dev/null
else
  docker run -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker:/var/lib/docker --rm martin/docker-cleanup-volumes 2> /dev/null
fi
