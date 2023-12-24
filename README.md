# Proyecto web coorporativa ConchiCoaching

Landing page con sistema de blog y página de contato. Panel de admin para gestionar los contactos y creación de post en el blog para ciertos usuarios

DJANGO


- Creación de la carpeta .ebextensions
- Introducción del profile AWS en mac ~/.aws/credentials. En mi caso añado esto: 


[conchicoaching]
aws_access_key_id=**********
aws_secret_access_key==**********

- eb init --profile conchicoaching
- eb create conchicoaching-env
- eb deploy
- Con eb status podemos ver la url del entorno: conchicoaching-env.eba-2mj8jpp8.eu-west-3.elasticbeanstalk.com

Preparacion del dominio:

1) El dominio por si solo no es "nada" en AWS. Hay que crear una zona alojada para este dominio. 
2) La zona alojada se crea por tanto para: conchicoaching.es. Una zona alojada pública.
3) La zona alojada se crear con los NS por defecto de AWS, los cuales hay que mantener

Ahora es importante enlazarlo con un dominio, y para ello, crear tmb un certificado. 

1) En Certificate Manager de AWS, creamos un certificado asociado a este dominio. Un certificado público para el dominio: conchicoaching.es y con validación DNS. El resto de campos los dejamos igual
2) Al solicitarlo, y entrar en el, vemos como está pendiente de validación. AWS necesita validar estos CNAME en el dominio (zona alojada). Por lo tanto hay que crear estos registros en la zona
3) Tras la creación, esperamos unos segundos a su propagación. El certificado ya estará validado

Ahora toca enlazar este dominio a nuestro entorno

1) Creamos un nuevo registro de tipo A en la zona alojada
2) Aplicamos la opcion de Alias
3) Elegimos alias de entorno de Elastic Beanstalk. Nuestra zona, y nuestro entorno

