# missed-block-monitoring
some script to automatically install and run tenderduty
#Auto installer
wget https://raw.githubusercontent.com/alfset/missed-block-monitoring/main/tenderduty.sh && chmod +x tenderduty.sh && ./tenderduty.sh

#manual install Using Docker

Install docker

mkdir tenderduty && cd tenderduty

docker run --rm ghcr.io/blockpane/tenderduty:latest -example-config >config.yml
# edit config.yml and add chains, notification methods etc.
docker run -d --name tenderduty -p "8888:8888" -p "28686:28686" --restart unless-stopped -v $(pwd)/config.yml:/var/lib/tenderduty/config.yml ghcr.io/blockpane/tenderduty:latest
docker logs -f --tail 20 tenderduty
