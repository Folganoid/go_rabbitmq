docker run -d -h node-1.rabbit --name rabbit -p "4369:4369" -p "5672:5672" -p "15672:15672" -p "25672:25672" -p "35197:35197" -e "RABBITMQ_USE_LONGNAME=true" -e "RABBITMQ_LOGS=/var/log/rabbitmq/rabbit.log" -v /data:/var/lib/rabbitmq -v /data/logs:/var/log/rabbitmq rabbitmq:3.6.6-management

# delete guest
docker exec rabbit rabbitmqctl delete_user guest

# Admin user
docker exec rabbit rabbitmqctl add_user fg 999
docker exec rabbit rabbitmqctl set_user_tags fg administrator

# Application user
docker exec rabbit rabbitmqctl add_user go_app 000
docker exec rabbit rabbitmqctl set_permissions -p / go_app ".*" ".*" ".*"
