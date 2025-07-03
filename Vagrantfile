Vagrant.configure("2") do |config|

  # VM1 - cu box version de Ubuntu
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "ubuntu/focal64"
    vm1.vm.hostname = "vm1"
    # aloc cate o adresa IP pt fiecare masina in parte
    vm1.vm.network "private_network", ip: "192.168.50.11"

    # Dezactivează firewall pentru a permite ping
    vm1.vm.provision "shell", inline: <<-SHELL
      echo "[VM1] Disabling firewall..."
      sudo ufw disable || true

      apt-get update
      apt-get install -y docker.io docker-compose

      # director pentru Docker Compose
      mkdir -p /vagrant/docker

      # Creeaza fisierul docker-compose.yml
      cat > /vagrant/docker/docker-compose.yml << EOF
version: '3.8'
services:
  traefik:
    image: traefik:v2.8
    command:
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - proxy

  lidarr:
    image: lscr.io/linuxserver/lidarr
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.lidarr.rule=Host(`lidarr.local`)"
    networks:
      - proxy

  sonarr:
    image: lscr.io/linuxserver/sonarr
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.sonarr.rule=Host(`sonarr.local`)"
    networks:
      - proxy

  radarr:
    image: lscr.io/linuxserver/radarr
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.radarr.rule=Host(`radarr.local`)"
    networks:
      - proxy

  tautulli:
    image: lscr.io/linuxserver/tautulli
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.tautulli.rule=Host(`tautulli.local`)"
    networks:
      - proxy

  overseerr:
    image: lscr.io/linuxserver/overseerr
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.overseerr.rule=Host(`overseerr.local`)"
    networks:
      - proxy

  jackett:
    image: lscr.io/linuxserver/jackett
    environment:
      - PUID=1000
      - PGID=1000
    labels:
      - "traefik.http.routers.jackett.rule=Host(`jackett.local`)"
    networks:
      - proxy

networks:
  proxy:
    driver: bridge
EOF

      cd /vagrant/docker
      docker-compose up -d
    SHELL
  end

  # VM2 - cu box version de Ubuntu
  config.vm.define "vm2" do |vm2|
    vm2.vm.box = "ubuntu/focal64"
    vm2.vm.hostname = "vm2"
    vm2.vm.network "private_network", ip: "192.168.50.12"
  end

  # VM3 - cu box version de Ubuntu
  config.vm.define "vm3" do |vm3|
    vm3.vm.box = "ubuntu/focal64"
    vm3.vm.hostname = "vm3"
    vm3.vm.network "private_network", ip: "192.168.50.13"
  end

  # VM4 - cu box version de Ubuntu
  config.vm.define "vm4" do |vm4|
    vm4.vm.box = "ubuntu/focal64"
    vm4.vm.hostname = "vm4"
    vm4.vm.network "private_network", ip: "192.168.50.14"
  end

  # VM5 - cu box version de Ubuntu
  config.vm.define "vm5" do |vm5|
    vm5.vm.box = "ubuntu/focal64"
    vm5.vm.hostname = "vm5"
    vm5.vm.network "private_network", ip: "192.168.50.15"
  end

end
