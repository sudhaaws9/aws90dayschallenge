    aws ec2 describe-regions > output.json

    ls

    .\output.json

    aws ec2 describe-regions --query "Regions[0]"

    aws ec2 describe-regions --query "Regions[-1]"

    aws ec2 describe-regions --query "Regions[::1].RegionName"

    aws ec2 describe-regions --query "Regions[].Endpoint"

    aws ec2 describe-regions --query "regions[].Endpoint | [0]"

    aws ec2 describe-regions --query "Regions[].Endpoint | [::2]"

    aws ec2 describe-instances

    aws ec2 describe-instances > instances.json

    aws ec2 describe-instances --query "Reservations[].Instances[*]"

    aws ec2 describe-instances --query "Reservations[].Instances[*].ImageId"

    aws ec2 describe-instances --query "Reservations[].Instances[*].ImageId | [0]"
    aws ec2 describe-instances --query "Reservations[].Instances[*].ImageId | [*]"

    aws ec2 describe-instances --query "Reservations[].Instances[*].[ImageId,InstanceType]"

    aws ec2 describe-instances --query "Reservations[].Instances[*].{nameof ami:ImageId,typeofInstance:InstanceType}"

    aws ec2 describe-images --owner amazon > images.json

    aws ec2 describe-images --owner amazon --query "length(Images)"










