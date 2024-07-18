FROM node:16.18

ENV PORT=3000
#frontend dockerfile
COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]