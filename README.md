# Notejam Cloud Infrastructure
The Notejam application is running using python implementation on Django framework

The above cloudformation script creates the required Infrastructure within AWS and deploys the Notejam application.

Prerequisites:
1) Make sure aws-cli is installed and configure aws with correct credentials & region
2) git clone https://github.com/prasannatumu/Notejam.git
3) ./stack-create.sh    (creates the infrastructure and deploys Notejam application)

Note:
The below commands in the 'UserData' section of file 'servers.yaml' deploys the Notejam application.

        Fn::Base64: !Sub |
            #!/bin/bash
            yum update -y
            yum install -y git
            git clone https://github.com/komarserjio/notejam.git
            cd notejam/django/
            virtualenv -p /usr/bin/python venv
            source venv/bin/activate
            pip install -r requirements.txt
            cd notejam/
            ./manage.py syncdb --noinput
            echo "from django.contrib.auth.models import User; User.objects.create_superuser('admin', 'admin@example.com', 'pass')" | python manage.py shell
            ./manage.py migrate
            ./manage.py runserver

Please refer to 'NoteJam presentation.pptx' for more details about the architecture.
