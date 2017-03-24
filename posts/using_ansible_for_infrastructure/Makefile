web.pub:
	ssh-keygen -t rsa -C web -f ./web -P ''

ec2.py:
	curl -o ec2.py \
	  https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
	chmod u+x ec2.py

ec2.ini:
	curl -o ec2.ini \
	  https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini

build: web.pub
	AWS_PROFILE=playground \
	AWS_REGION=eu-west-1 \
	ansible-playbook build-infra.yml

provision: ec2.py ec2.ini web.pub
	AWS_PROFILE=playground \
	AWS_REGION=eu-west-1 \
	ANSIBLE_HOST_KEY_CHECKING=false \
	ANSIBLE_PRIVATE_KEY_FILE=web \
	ansible-playbook -i ec2.py provision-infra.yml
