FROM alpine/git AS source
RUN git clone --depth 1 https://github.com/wayou/t-rex-runner.git /src && rm -rf /src/.git

FROM node:lts-alpine
RUN npm install -g http-server
WORKDIR /app
COPY --from=source /src .
EXPOSE 8080
CMD ["http-server", "-p", "8080"]
