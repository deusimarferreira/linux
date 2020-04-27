# Gunicorn

~~~sh
gunicorn --workers=4 --bind=0.0.0.0 \
  --access-logfile=/opt/git/vlabs-py3270/gunicorn-access.log \
  --error-logfile=/opt/git/vlabs-py3270/gunicorn-error.log \
  --limit-request-line=0 --limit-request-fields=32768 \
  --limit-request-field_size=0 \
  --log-level=debug --timeout=5000 --keep-alive=240 wsgi:app &
~~~
