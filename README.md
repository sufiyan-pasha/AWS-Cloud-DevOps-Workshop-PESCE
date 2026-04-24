# AWS-Cloud-DevOps-Workshop-PESCE

Commands Used in the Workshop:
```
apt update -y
apt upgrade -y
apt install apache2 -y
git clone https://github.com/yeshwanthlm/AWS-Cloud-DevOps-Workshop-PESCE.git
cd AWS-Cloud-DevOps-Workshop-PESCE/
ls -lrt
mv * /var/www/html/
```

GitHub Action Script:

```yaml
name: Push-to-EC2

# Trigger deployment only on push to main branch
on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy to EC2 on main branch push
    runs-on: ubuntu-latest

    steps:
      - name: Checkout the files
        uses: actions/checkout@v2

      - name: Deploy to Server 1
        uses: easingthemes/ssh-deploy@main
        env:
          SSH_PRIVATE_KEY: ${{ secrets.EC2_SSH_KEY }}
          REMOTE_HOST: ${{ secrets.HOST_DNS }}
          REMOTE_USER: ${{ secrets.USERNAME }}
          TARGET: ${{ secrets.TARGET_DIR }}

      - name: Executing remote ssh commands using ssh key
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.HOST_DNS }}
          username: ${{ secrets.USERNAME }}
          key: ${{ secrets.EC2_SSH_KEY }}
          script: |
            sudo apt-get -y update
            sudo apt-get install -y apache2
            sudo systemctl start apache2
            sudo systemctl enable apache2
            cd home
            sudo mv * /var/www/html
```
Blog: https://dev.to/aws-builders/deploy-resume-to-aws-ec2-using-github-actions-4hog

Follow me:
* YouTube: https://www.youtube.com/@TechWithYeshwanth/videos
* Follow our GitHub here: https://github.com/yeshwanthlm
* Follow my blog here: https://dev.to/yeshwanthlm/
* Follow me on Instagram: https://www.instagram.com/techwithyeshwanth/
* Personal LinkedIn: https://www.linkedin.com/in/yeshwanth-l-m/
* Book 1:1 Meeting with me: https://topmate.io/techwithyeshwanth
* PPT used in the session: [AWS CloudDevOps Workshop @ PESCE .pdf](https://github.com/user-attachments/files/27062169/AWS.CloudDevOps.Workshop.%40.PESCE.pdf)


Please provide your valuable feedback: https://forms.gle/Wzz4S6miXxMEuueUA



