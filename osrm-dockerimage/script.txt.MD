docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-extract -p /opt/car.lua /data/data.osm.pbf
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-partition /data/data.osrm 
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-customize /data/data.osrm 

docker build -t registry.heroku.com/olamundo-fw/image .
docker build -t registry.heroku.com/olamundo-fw/web .
docker push registry.heroku.com/olamundo-fw/image
docker push registry.heroku.com/olamundo-fw/web
heroku container:release web -a olamundo-fw  