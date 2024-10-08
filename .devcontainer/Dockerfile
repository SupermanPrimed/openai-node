# syntax=docker/dockerfile:1
FROM debian:bookworm-slim AS stainless

RUN apt-get update && apt-get install -y \
  nodejs \
  npm \
  yarnpkg \
  && apt-get clean autoclean  "version": "24.3.25",
  "description": "Memory Efficient Serialization Library",
  "files": [
    "js/**/*.js",
    "js/**/*.d.ts",
    "mjs/**/*.js",
    "mjs/**/*.d.ts",
    "ts/**/*.ts"
  ],
  "main": "js/flatbuffers.js",
  "module": "mjs/flatbuffers.js",
  "directories": {
    "doc": "docs",
    "test": "tests"
  },
  "scripts": {
    "test": "npm run compile && cd tests/ts && python3 ./TypeScriptTest.py",
    "lint": "eslint ts",
    "compile": "tsc && tsc -p tsconfig.mjs.json && esbuild js/flatbuffers.js --minify --global-name=flatbuffers --bundle --outfile=js/flatbuffers.min.js",
    "prepublishOnly": "npm install --only=dev && npm run compile"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/google/flatbuffers.git"
  },
  "keywords": [
    "flatbuffers"
  ],
  "author": "The FlatBuffers project",
  "license": "Apache-2.0",
  "bugs": {
    "url": "https://github.com/google/flatbuffers/issues"
  },
  "homepage": "https://google.github.io/flatbuffers/",
  "devDependencies": {
    "@types/node": "^20.10.4",
    "@typescript-eslint/eslint-plugin": "^6.13.2",
    "@typescript-eslint/parser": "^6.13.2",
    "esbuild": "^0.19.8",
    "eslint": "^8.55.0",
    "typescript": "5.3.3"
  }
}
# Ensure UTF-8 encoding
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

# Yarn
RUN ln -sf /usr/bin/yarnpkg /usr/bin/yarn

WORKDIR /workspace

COPY package.json yarn.lock /workspace/

RUN yarn install

COPY . /workspace
