# Use an official Python runtime as a parent image
FROM docker.io/python:3-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

RUN pip install opentelemetry-distro opentelemetry-exporter-otlp

RUN opentelemetry-bootstrap --action=install

# Make port 5000 available to the world outside this container
EXPOSE 5000

ENV OTEL_EXPORTER_OTLP_ENDPOINT="http://otel-collector:4317"
# ENV OTEL_EXPORTER_OTLP_PROTOCOL: http/protobuf
ENV OTEL_EXPORTER_OTLP_PROTOCOL=grpc
ENV OTEL_METRICS_EXPORTER="otlp"
ENV OTEL_TRACES_EXPORTER="otlp"
ENV OTEL_LOGS_EXPORTER="otlp"
ENV OTEL_SERVICE_NAME=student
ENV OTEL_LOG_LEVEL=debug



# Run app.py when the container launches
# CMD ["flask", "run", "-p", "5000"]
CMD ["opentelemetry-instrument", "python","student.py"]