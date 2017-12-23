=====
django_bot_crawler_blocker
=====

This is a simple Django app to block the IP addresses which sends too many hits to your application.
You can decide the number of hits that are allowed per IP address in defined time.


Quick start
-----------

1. Add "django_bot_crawler_blocker" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = [
        ...
        'django_bot_crawler_blocker',
    ]


2. Add 'CrawlerBlockerMiddleware' to your middleware classes in settings.py file::

    MIDDLEWARE = [
        'django_bot_crawler_blocker.django_bot_crawler_middleware.CrawlerBlockerMiddleware',
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
    ]

   'CrawlerBlockerMiddleware' can be and should be first middleware as we need to make sure IP check is the very first
    thing in processing request.


3. If cache settings are not defined in your settings.py file, then you need to add below lines to your settings.py file::

    CACHES = {
        'default': {
            'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
            'LOCATION': 'cache_table',
        }
    }

   Make sure you have database settings configured. Run the below command to create cache_table in database::

    'python manage.py createcachetable'

   You may choose whatever cache backend you want to use.


4. (optional) Set variables in MAX_ALLOWED_HITS_PER_IP and IP_HITS_TIMEOUT in settings.py file::

    MAX_ALLOWED_HITS_PER_IP = 2000  # max allowed hits per IP_TIMEOUT time from an IP. Default 2000.
    IP_HITS_TIMEOUT = 60  # timeout in seconds for IP in cache. Default 60.

   To test on local system, set these values to very low, e.g. IP_HITS_TIMEOUT = 30 and MAX_ALLOWED_HITS_PER_IP = 2.
   Restart the server and send requests frequently. After two requests you will start receiving 403 error.
   If not defined in settings file, default values will be used.


5. In case of any query or issue, please feel free to reach out to me. Email provided in MANIFEST file.




