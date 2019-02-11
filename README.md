# Dive deep into Android Services

## When use Services?

1. Performing operations that need to continue even if the user leaves the application’s activities, like a long download (as seen with the Play Store) or playing music (as seen with Android music apps)
2. Performing operations that need to exist regardless of activities coming and going, such as maintaining a chat connection in support of a chat application
3. Providing a local API to remote APIs, such as might be provided by a Web service
4. Performing periodic work without user intervention, akin to cron jobs or Windows scheduled tasks”


## Comunicating between Services and UI?
#### Use LocalBroadcastManager
This is designed to offer an event bus with a feel very similar to classic broadcast Intent objects, but local to your process. Not only does this avoid IPC overhead, but it improves security, as other apps have no means of spying on your internal communications.


## Time
### Limitation: 
on Android 8.0+, a started service like this can run for only one minute. After that, Android will stop the service. That will not terminate our background thread immediately, but it will make it far more likely that Android will terminate our entire process, taking our thread and download with it.
### Solution:
Make the service be a “foreground service”


## Staying awake
### Limitation:
Even if our work is certain to take less than a minute, we may run into another problem: the device might fall asleep. When the screen turns off, by default, Android will power down the CPU, suspending all running processes.
### Solution:
JobIntentService works around this by way of a “wakelock”: a request to the OS to keep the device awake, even though the screen turns off.
