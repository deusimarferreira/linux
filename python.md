
## Flask
~~~sh
export PATH=${PATH}:/opt/git/vlabs-py3270/x3270/suite3270-3.6/obj/x86_64-unknown-linux-gnu/s3270
export FLASK_APP=run.py
export FLASK_ENV=production

python3.8 -m flask run --no-debugger --no-reload --host 0.0.0.0 &
~~~

## Gunicorn

~~~sh
# -t 144000 --max-requests=1 
gunicorn --workers=4 --bind=0.0.0.0 \
  --access-logfile=/opt/git/vlabs-py3270/gunicorn-access.log \
  --error-logfile=/opt/git/vlabs-py3270/gunicorn-error.log \
  --limit-request-line=0 --limit-request-fields=32768 \
  --limit-request-field_size=0 \
  --log-level=debug --timeout=5000 --keep-alive=240 wsgi:app &
~~~
