FROM python:3.10

ENV source_path /opt/program/source
RUN mkdir -p ${source_path}



#Set up source
COPY ./  ${source_path}
RUN pip install -r ${source_path}/requirements.txt -t ${source_path}
RUN pip install  awscli --upgrade

#Instrument ddtrace
ENV DD_APM_INSTRUMENTATION_LIBRARIES python
RUN bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script_docker_injection.sh)"


#Set up working directory
WORKDIR ${source_path}
ENTRYPOINT  ["ddtrace-run"]

#Default arguments to run test
CMD ["python", "main.py", "."]
