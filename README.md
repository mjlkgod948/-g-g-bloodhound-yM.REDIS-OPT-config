# -g-g-bloodhound-yM.REDIS-OPT-config



       'sWhy is Celery useful?
Task queues and the Celery implementation in particular are one of the trickier parts of a Python web application stack to understand.

If you are a junior developer it can be unclear why moving work outside the HTTP request-response cycle is important. In short, you want your WSGI server to respond to incoming requests as quickly as possible because each request ties up a worker process until the response is finished. Moving work off those workers by spinning up asynchronous jobs as tasks in a queue is a straightforward way to improve WSGI server response times.

What's the difference between Celeryd and Celerybeat?
Celery can be used to run batch jobs in the background on a regular schedule. A key concept in Celery is the difference between the Celery daemon (celeryd), which executes tasks, Celerybeat, which is a scheduler. Think of Celeryd as a tunnel-vision set of one or more workers that handle whatever tasks you put in front of them. Each worker will perform a task and when the task is completed will pick up the next one. The cycle will repeat continously, only waiting idly when there are no more tasks to put in front of them.

Celerybeat on the other hand is like a boss who keeps track of when tasks should be executed. Your application can tell Celerybeat to execute a task at time intervals, such as every 5 seconds or once a week. Celerybeat can also be instructed to run tasks on a specific date or time, such as 5:03pm every Sunday. When the interval or specific time is hit, Celerybeat will hand the job over to Celeryd to execute on the next available worker.

Celery tutorials and advice
Celery is a powerful tool that can be difficult to wrap your mind around at first. Be sure to read up on task queue concepts then dive into these specific Celery tutorials.

A 4 Minute Intro to Celery is a short introductory task queue screencast.

This blog post series on Celery's architecture, Celery in the wild: tips and tricks to run async tasks in the real world and dealing with resource-consuming tasks on Celery provide great context for how Celery works and how to handle some of the trickier bits to working with the task queue.

How to use Celery with RabbitMQ is a detailed walkthrough for using these tools on an Ubuntu VPS.

Celery - Best Practices explains things you should not do with Celery and shows some underused features for making task queues easier to work with.

Celery Best Practices is a different author's follow up to the above best practices post that builds upon some of his own learnings from 3+ years using Celery.

Common Issues Using Celery (And Other Task Queues) contains good advice about mistakes to avoid in your task configurations, such as database transaction usage and retrying failed tasks.

Asynchronous Processing in Web Applications Part One and Part Two are great reads for understanding the difference between a task queue and why you shouldn't use your database as one.

My Experiences With A Long-Running Celery-Based Microprocess gives some good tips and advice based on experience with Celery workers that take a long time to complete their jobs.

Checklist to build great Celery async tasks is a site specifically designed to give you a list of good practices to follow as you design your task queue configuration and deploy to development, staging and production environments.

Heroku wrote about how to secure Celery when tasks are otherwise sent over unencrypted networks.

Unit testing Celery tasks explains three strategies for testing code within functions that Celery executes. The post concludes that calling Celery tasks synchronously to test them is the best strategy without any downsides. However, keep in mind that any testing method that is not the same as how the function will execute in a production environment can potentially lead to overlooked bugs. There is also an open source Git repository with all of the source code from the post.

Rollbar monitoring of Celery in a Django app explains how to use Rollbar to monitor tasks. Super useful when workers invariably die for no apparent reason.

3 Gotchas for Working with Celery are things to keep in mind when you're new to the Celery task queue implementation.

Dask and Celery compares Dask.distributed with Celery for Python projects. The post gives code examples to show how to execute tasks with either task queue.

Python+Celery: Chaining jobs? explains that Celery tasks should be dependent upon each other using Celery chains, not direct dependencies between tasks.

Celery with web frameworks
Celery is typically used with a web framework such as Django, Flask or Pyramid. These resources show you how to integrate the Celery task queue with the web framework of your choice.

How to Use Celery and RabbitMQ with Django is a great tutorial that shows how to both install and set up a basic task with Django.

Miguel Grinberg wrote a nice post on using the task queue Celery with Flask. He gives an overview of Celery followed by specific code to set up the task queue and integrate it with Flask.

Setting up an asynchronous task queue for Django using Celery and Redis is a straightforward tutorial for setting up the Celery task queue for Django web applications using the Redis broker on the back end.

A Guide to Sending Scheduled Reports Via Email Using Django And Celery shows you how to use django-celery in your application. Note however there are other ways of integrating Celery with Django that do not require the django-celery dependency.

Flask asynchronous background tasks with Celery and Redis combines Celery with Redis as the broker and Flask for the example application's framework.

Celery and Django and Docker: Oh My! shows how to create Celery tasks for Django within a Docker container. It also provides some

Asynchronous Tasks With Django and Celery shows how to integrate Celery with Django and create Periodic Tasks.

Getting Started Scheduling Tasks with Celery is a detailed walkthrough for setting up Celery with Django (although Celery can also be used without a problem with other frameworks).

Asynchronous Tasks with Falcon and Celery configures Celery with the Falcon framework, which is less commonly-used in web tutorials.

Custom Celery task states is an advanced post on creating custom states, which is especially useful for transient states in your application that are not covered by the default Celery configuration.

Asynchronous Tasks with Django and Celery looks at how to configure Celery to handle long-running tasks in a Django app.

Celery deployment resources
Celery and its broker run separately from your web and WSGI servers so it adds some additional complexity to your deployments. The following resources walk you through how to handle deployments and get the right configuration settings in place.

How to run celery as a daemon? is a short post with the minimal code for running the Celery daemon and Celerybeat as system services on Linux.
Do you want to learn more about task queues, or another topic?
