### Message Queue Consumer with python
#rabbitmq

For Creating a consumer from rabbitmq a package called pika is used.
- Define a connection.
- Mention the queue that you would like to listen to.
- Create a function which should be executed when message is received.
- You can choose to acknowledge back immediatley or acknowledge back after processing.

```python
import os  
import pika  
import sys  
  
  
def main():  
    connection = pika.BlockingConnection(pika.ConnectionParameters(host='localhost'))  
    channel = connection.channel()  
  
    #channel.queue_declare(queue='testRunner')  
  
    def callback(ch, method, properties, body):  
        print(" [x] Received %r" % body.decode())  
  
    channel.basic_consume(queue='testRunner', on_message_callback=callback, auto_ack=True)  
  
    print(' [*] Waiting for messages. To exit press CTRL+C')  
    channel.start_consuming()  
  
  
if __name__ == '__main__':  
    try:  
        main()  
    except KeyboardInterrupt:  
        print('Interrupted')  
        try:  
            sys.exit(0)  
        except SystemExit:  
            os._exit(0)
```

### Requirements.txt
```requirements
pika
```