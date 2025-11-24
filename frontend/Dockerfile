FROM node:18 as build

WORKDIR /app

COPY package*.json ./
RUN npm install
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL


# Accept build-time env variable from Cloud Run
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

COPY . .

RUN npm run build

# --- Production stage ---
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
