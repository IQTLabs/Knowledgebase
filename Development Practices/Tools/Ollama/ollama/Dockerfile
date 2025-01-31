FROM ollama/ollama:latest

# need this for a healthcheck to run
RUN apt update && apt-get install -y curl

COPY startup.sh .

ENTRYPOINT ["./startup.sh"]