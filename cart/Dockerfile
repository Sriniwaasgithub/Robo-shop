FROM node:14
# ENV INSTANA_AUTO_PROFILE true
RUN groupadd -r cart && useradd -r -m -g cart cart
EXPOSE 8080
WORKDIR /opt/server
RUN chown -R cart:cart /opt/server
USER cart
COPY package.json /opt/server/
RUN ls -lrt
RUN npm install
COPY server.js /opt/server/
CMD ["node", "server.js"]

