NAME 			:= inception
DOCKER-COMPOSE 	:= ./srcs/docker-compose.yaml
ENV_FILE 		:= ./srcs/.env
VOLUMES_DIR 	:= /home/engirald42/data

all: build

build: setup
	sudo docker compose -f $(DOCKER-COMPOSE) --env-file $(ENV_FILE) up -d --build

start:
	sudo docker compose -f $(DOCKER-COMPOSE) start

stop:
	sudo docker compose -f $(DOCKER-COMPOSE) stop

down:
	sudo docker compose -f $(DOCKER-COMPOSE) down 

ps:
	sudo docker ps

clean: stop
	sudo docker compose -f $(DOCKER-COMPOSE) down

fclean: clean
	sudo docker compose -f $(DOCKER-COMPOSE) down --remove-orphans
	sudo docker compose -f $(DOCKER-COMPOSE) down --volumes


prune:
	sudo docker system prune -af
	sudo docker image prune -f
	sudo rm -rf $(VOLUMES_DIR)
	sudo sed -i '1s/engirald42.42.fr www.engirald.42.fr/localhost/' '/etc/hosts'
	sudo cat /etc/hosts | head -n 1

re: fclean all
	

images:
	sudo docker images -qa

network:
	sudo docker network ls

volume:
	sudo docker volume ls

logs:
	sudo docker logs -t -f $$(docker compose -f $(DOCKER-COMPOSE) ps -q nginx)

setup:
	sudo mkdir -p $(VOLUMES_DIR)/website
	sudo mkdir -p $(VOLUMES_DIR)/database
	sudo bash ./srcs/requirements/tools/setup.sh

help:
	sudo echo $(OR)Inception $(PK)help$(RES)

.PHONY: all build start stop down ps clean fclean \
		re images network volume logs setup help

