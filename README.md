# DEV-IMPACT-03-DEPLOY-AWS-EBS


## Como rodar o projeto?

```
git clone https://github.com/jobconvo/DEV-IMPACT-03-DEPLOY-AWS-EBS.git dev-impact-03-deploy-aws-ebs
cd dev-impact-03-deploy-aws-ebs
```

## Backend

O backend foi feito em Django baseado no repo

https://github.com/jobconvo/DEV-IMPACT-01-DRF

```
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python contrib/env_gen.py
python manage.py migrate
python manage.py createsuperuser --username="admin" --email=""
```

No Admin crie seu Token. Ou pelo terminal:

```
python manage.py drf_create_token admin
```


## Frontend

O frontend foi feito em VueJS baseado no repo

https://github.com/jobconvo/DEV-IMPACT-02-VUE

```
cd frontend
npm install
npm run serve
```

Crie um arquivo `.env` na pasta frontend e escreva

```
cat << EOF > .env
VUE_APP_TOKEN=seu_token_criado_pelo_backend
EOF
```



