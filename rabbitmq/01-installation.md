### Installing RabbitMQ
- Before installing we need to install ErLang
- Download and install Erlang from https://www.erlang.org/downloads
- Downoad the correct version of ErLang, RabbitMQ and compatable Erlang versions are present at https://www.rabbitmq.com/which-erlang.html
- Download Rabbit MQ from https://www.rabbitmq.com/download.html
- For windows it will be a executable file install it.

> RabbitMQ management portal is available will be on url http://www.localhost:15672

- To enable management console
- Navigate to the location where rabbitmq is installed.
- Open `sbin` folder in command prompt.
- Run `rabbitmq-plugins.abt enable rabbitmq_management`
- If no errors occur you should be able to see management console on http://www.localhost:15672