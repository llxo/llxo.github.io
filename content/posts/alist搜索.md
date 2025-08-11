+++
title = 'alist搜索'
date = 2025-08-11T18:23:44+08:00
draft = false
+++

在alist/openlist上使用meilisearch索引

[openlist的相关文档](https://doc.openlist.team/guide/advanced/search#%E4%B8%8D%E5%90%8C%E6%90%9C%E7%B4%A2%E7%B4%A2%E5%BC%95%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E5%BC%82)

#### 使用docker compose

docker-compose.yml

```
version: '3.3'
services:
  openlist:
    image: 'openlistteam/openlist:latest'
    container_name: openlist
    volumes:
      - '/etc/openlist:/opt/openlist/data'
    ports:
      - '5244:5244'
    environment:
      - PUID=0
      - PGID=0
      - UMASK=022
      - MEILISEARCH_HOST=http://meilisearch:7700  
      - MEILISEARCH_API_KEY=MEILISEARCH_MASTER_KEY
    restart: unless-stopped

  meilisearch:
    image: getmeili/meilisearch:v1.9.1
    container_name: meilisearch
    volumes:
      - ./meili_data:/meili_data
    environment:
      MEILI_MASTER_KEY: 'MEILISEARCH_MASTER_KEY'
    ports:
      - "7700:7700"
    restart: always
    command: meilisearch --schedule-snapshot --snapshot-dir /meili_data/snapshots
```
重启就行了，记得改`MEILISEARCH_MASTER_KEY`

meilisearch新版不行，索引不了

#### alist/openlist 设置

进入管理页

`https://yourdomain.com/@manage/indexes`或`https://yourip:5244/@manage/indexes`

搜索索引选择Meilisearch

保存，重建索引