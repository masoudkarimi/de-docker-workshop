# base docker image that we will build on
FROM python:3.13-slim

# setup our image by installing prerequisites; pandas and pyarrow
RUN pip install pandas pyarrow

# set the working directory in the image
WORKDIR /app

# copy the pipeline.py file into the image
COPY pipeline.py pipeline.py

ENTRYPOINT [ "python", "pipeline.py" ]

CMD ["python", "pipeline.py"]
