FROM python:3.9-slim
WORKDIR /app


COPY appy.py appy.py


RUN pip install flask gunicorn

EXPOSE 5000

ENTRYPOINT ["gunicorn"]

CMD ["--workers", "2", "--bind", "0.0.0.0:5000", "appy:app"]
