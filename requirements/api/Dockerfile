# Use GDAL as base to have most of the GeoSpatial functionality installed by default
FROM ghcr.io/osgeo/gdal:alpine-normal-latest

RUN mkdir /app
WORKDIR /app

RUN apk add --no-cache \
	python3 \
	py3-pip \
	postgresql-client \
	geos

RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin/:$PATH"

COPY --chmod=+x tools/api_entrypoint.sh /usr/local/sbin/
COPY app/app /app/app
COPY app/api /app/api
COPY app/manage.py /app/manage.py
COPY app/requirements.txt /app/requirements.txt
RUN pip install -Ur requirements.txt

EXPOSE 8000

ENTRYPOINT ["api_entrypoint.sh"]
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
