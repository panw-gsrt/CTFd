![](https://raw.githubusercontent.com/panw-gsrt/CTFd/master/CTFd/static/img/logo.png)
====

Install: 
 1. `./prepare.sh` to install dependencies using apt.
 2. Modify [CTFd/config.py](https://github.com/isislab/CTFd/blob/master/CTFd/config.py) to your liking.
 3. Use `python serve.py` in a terminal to drop into debug mode.
 4. [Here](https://github.com/isislab/CTFd/wiki/Deployment) are some deployment options

Install gunicorn from apt repository: sudo apt-get install gunicorn
Create gunicorn config file for CTFd: sudo vim /etc/gunicorn.d/ctfd
CONFIG = {
    'mode': 'wsgi',
    'working_dir': '/home/ubuntu/CTFd',
      'python': '/usr/bin/python',
    'user': 'ubuntu',
    'group': 'ubuntu',
    'args': (
        '--bind=0.0.0.0:8000',
        '--workers=1',
        '--umask=0027',
        '--log-level=info',
        '--access-logfile=/var/log/gunicorn/ctfd_access.log',
        'CTFd:create_app()',
    ),
}

service gunicorn start
