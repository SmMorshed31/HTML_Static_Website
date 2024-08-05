This repo contains the files I created to make a website using html and css. I used a website template and in my server.py, I specified the host to '0.0.0.0' so that any IP address can access the website for my testing. 

After editing the files, I then created an S3 bucket to store these files and create a host a static website. I wrote a bucket policy to make all the files readable and made the bucket public. 
The issue I had was that the static website would not display a lot of the assests and images I had. 
Most likely due to the server.py file which required more dynamic hosting, which is where EC2 came in. 

I created an ec2 instance on Amazon Linux, t2 micro, created default VPC and subnet, as well as the security groups with inbound rules of HTTP(port 80) and HTTPS(port 443) along side SSH(port 22) and custom tcp(port 5000) where they can be accessed from anywhere('0.0.0.0'). 
I also created the keypair and then launched the instance. From there, I created an IAM role with EC2 access and create a role that allowed ec2 to have full s3 access and attached the role to my instance. 

Now I needed to SSH into my instance so I could establish the instance as a server to then load up my webpage. After updating the instance cli, I downloaded python, boto3, flask, aws cli, as well as the s3 mount software onto the instance. 
The s3 mount software was necessary to transfer the files in my s3 bucket to a directory in the instance. 

  aws s3 cp s3://your-bucket-name/path/to/server.py s3mount/ #this is the code I used to mount my s3 files into a directory. Replace the "your-bucket-name" with my bucket name which was sm-morshed-website. 

I then cd s3mount and did python3 server.py and it created a server. From there I took the public address given to the instance and added :5000 to the end of it and I was able to load up my website through an EC2 instance with an S3 bucket connected to it. 

  
