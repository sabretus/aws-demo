# AWS Demo
 1. Основний сайт амазона https://aws.amazon.com
 2. Мають безкоштовний план free-tier https://aws.amazon.com/free/ в який входить мінімальний набір сервісів, але при реєстрації буде вимагатись кредитка з якої тимчасово залокається 1 долар.
 3. Після реєстрації потрібно створити юзера для якого можна буде згенерити ключі і використовувати їх для АРІ або CLI, робиться це в меню IAM -> Users -> Create new users, для юзера також треба створити роль до якої налаштовуються певні полісі, таким чином ми сетаємо доступ для користувача. Зауважте чекбокс Generate an access key for each user і обовязково збережіть Access key ID i Secret.
 4. Потрібно заінсталити локально CLI, це робиться командою `pip install awscli --ignore-installed six` (http://docs.aws.amazon.com/cli/latest/userguide/installing.html)
 5. Потім в терміналі потрібно пройти просте налаштування CLI використовуючи команду `aws configure`, вона створить папку .aws в нашій хоум директорії.
 6. Далі в потрібному нам регіоні ми створюємо пару ссш ключів які автоматично додадуться для юзера ec2-user при створенні інстансу, для цього ідем в меню EC2 -> Key Pairs
 7. Для перевірки роботи CLI можна запустити команду яка порахує для нас можливі витрати на використані ресурси в темплейті і згенерує лінку на калькулятор `aws cloudformation estimate-template-cost --template-body file://./aws_demo/cloudformation/aws_jenkins_demo.json`
 8. І нарешті команда яка при наявності підготовленого темплейта створить нам інстанс і все засетапить `aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name TestJenkins --template-body file://./aws_demo/cloudformation/aws_jenkins_demo.json`
 9. Якщо все зроблено правильно, при поверненні до веб консолі https://console.aws.amazon.com/cloudformation/home ми побачимо наш стек в процесі створення.
 10. При успішному створенні стеку залишається піти до EC2 -> Instances і глянути який тимчасовий хостнейм засетаний для нашого нового сервера, туди можна залогінитись з ключем який ми створили на кроці 6. Команда ssh виглядатиме приблизно так `ssh ec2-user@ec2-52-90-252-89.compute-1.amazonaws.com -i jenkins_demo_key_us-east-1.pem`
 11. Останній крок перевірити чи відкриється наша веб сторінка http://ec2-52-90-252-89.compute-1.amazonaws.com
