FROM node:18.20

WORKDIR /app
COPY webapp/package*.json ./
# Install all dependencies for build 
RUN npm install

COPY webapp/ .
# Build the application using the local configuration.
RUN npm run build-local

# Run Stage
FROM node:18.20

WORKDIR /root/
COPY --from=build /app/dist ./build
COPY webapp/package*.json ./
COPY webapp/server.js ./

# Install only production dependencies
RUN npm install --only=production && npm install express

EXPOSE 3001

CMD [ "node", "server.js" ]
