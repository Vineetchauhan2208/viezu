FROM python:3.8
RUN apt-get update && apt-get install gcc wkhtmltopdf  ffmpeg libsm6 libxext6 cron sudo poppler-utils libgl1-mesa-glx poppler-data build-essential -y --no-install-recommends
RUN apt-get update && apt-get install python3-dev libpq-dev  -y
#RUN apt-get update && apt-get install tmux -y
#RUN mkdir -p /home/filemaker



# This instruction creates the Aiforyou user
#RUN addgroup --system jasiri && adduser --system --group jasiri

#set sudo permission for user 
#RUN echo "jasiri ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user && \
#    chmod 0440 /etc/sudoers.d/user
#WORKDIR /
WORKDIR /home/filemaker/
# This instruction prevents Python from writing .pyc files to Docker container for a good optimization.
ENV PYTHONDONTWRITEBYTECODE 1

# This instruction ensures that the python output is sent straight to container log without being first buffered.
ENV PYTHONUNBUFFERED 1


#COPY backend-filemaker .
COPY backend-code .
WORKDIR /home/filemaker/
RUN mkdir -p /home/filemaker/log
RUN touch  /home/filemaker/log/logs.log

#COPY extricator-321cbb03eda1.json extricator-321cbb03eda1.json
RUN pip install --upgrade pip
RUN pip install wheel
RUN pip install pandas openpyxl
#RUN pip install gunicorn
RUN pip install -r requirements.txt
COPY runner.sh runner.sh
RUN chmod +x runner.sh


#RUN cd /home/filemaker/ && tmux new -s worker -d  'celery -A filemaker worker -l info'

#Add Cron service
#COPY crontab /etc/cron.d/cool
#RUN chmod 0644 /etc/cron.d/cool

# This instruction chown all the files to the user
#RUN chown -R jasiri:jasiri /home/jasiri/
#RUN chown -R jasiri:jasiri /home/jasiri/
#RUN chmod -R 0777 /home/jasiri/
# This instruction changes to the aiforyou user
RUN  service cron start
#USER jasiri

## django pre-startup script
CMD ["/home/filemaker/runner.sh"]

#CMD ["/home/filemaker/celery -A filemaker worker -l info"]

