# 1. Builder
FROM node:24-alpine AS builder

#set directory
WORKDIR /app

#copy files
COPY package*.json .

#install dependencies
RUN npm install

#copy source code
COPY . .

#build next.js
RUN npm run build

#  2. Runner
FROM node:24-alpine AS runner

#set directory
WORKDIR /app

#environment variables for next.js
ENV NODE_ENV=production

#copy files
COPY --from=builder /app/.next/standalone ./.next/standalone
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public


#exspose port
EXPOSE 3000

#run app
CMD ["node", ".next/standalone/server.js"]



