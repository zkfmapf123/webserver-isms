# 웹취약점

## Todo

- [x] Directory Indexing
  - 디렉토리 구조를 가리키는 URL을 요청할때 웹서버 측에서 인덱스 페이지를 응답하여 발생하는 취약점
- [x] Server Token
  - Webserver version이 나타나는 취약점

## Nginx

> Nginx 설치

```sh
sudo yum update
sudo amazon-linux-extras install nginx1
sudo systemctl restart nginx

## conf 위치
cd /etc/nginx/nginc.conf
```

> Directory Indexing

```sh
    server {
	    server_name test.domain.com;

	    location = / {
    		root /var/datas/download;
        	autoindex off; ## 추가
	    }
    }
```

> Nginx 버전명시

```sh
server {

  listen 80;
  listen [::]:80;
  server_name My_Project_Name;

  # The nginx version is not specified in the response header Because of security.
  # default : on
  server_tokens off;    ## 추가

  location / {

    proxy_pass http://localhost:8080;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
  }
}
```

> After

![nginx](./public/nginx.png)

## Apache

> Apache 설치

```sh
sudo yum update
sudo yum install httpd

## conf 위치
cd /etc/httpd/conf
```

> Server Tokens

![apahche](./public/apahche.png)

> Directory indexing

![apache-2](./public/aparhce-2.png)

## Apache Referenece

- <a href="https://zetawiki.com/wiki/CentOS_%EC%95%84%ED%8C%8C%EC%B9%98_%EB%B3%B4%EC%95%88%EA%B6%8C%EC%9E%A5%EC%84%A4%EC%A0%95_ServerTokens_Prod,_ServerSignature_Off"> Apahche 권장사항 </a>
