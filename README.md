# kops

export NAME=mn450.k8s.local
export KOPS_STATE_STORE=s3://mn450kops.k8s.local


aws s3 rb s3://mn450.k8s.local

kops create cluster --zones us-east-1a --networking weave --master-size t2.medium --master-count 1 --node-size t2.micro --node-count 2 ${NAME}

kops create secret --name ${NAME} sshpublickey admin -i ~/.ssh/id_rsa.pub

kops update cluster ${NAME} --yes

kops validate cluster



to  delete kops cluster :

kops delete cluster --name=${NAME} --state=${KOPS_STATE_STORE} --yes
