# osrm-all
OSRM-project with osrm ready to heroku


# creating data files - path: osrm-backend
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-extract -p /opt/car.lua /data/data.osm.pbf
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-partition /data/data.osrm 
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-customize /data/data.osrm 


# deploy to heroku - path: osrm-dockerimage
docker build -t registry.heroku.com/olamundo-fw/image .
docker build -t registry.heroku.com/olamundo-fw/web .
docker push registry.heroku.com/olamundo-fw/image
docker push registry.heroku.com/olamundo-fw/web
heroku container:release web -a olamundo-fw