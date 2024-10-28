# AWS EC2 Terraform Template

This Terraform configuration creates an EC2 instance in AWS with all necessary networking components in the us-east-1 (North Virginia) region.

## Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) installed (version 0.12 or later)
- AWS CLI installed and configured with appropriate credentials
- Basic understanding of AWS services (EC2, VPC, etc.)

## Resources Created

This template creates the following AWS resources:

1. **VPC**
   - CIDR Block: 10.0.0.0/16
   - DNS hostnames enabled
   - DNS support enabled

2. **Public Subnet**
   - CIDR Block: 10.0.1.0/24
   - Availability Zone: us-east-1a

3. **Internet Gateway**
   - Attached to the VPC

4. **Route Table**
   - Routes traffic to the Internet Gateway
   - Associated with the public subnet

5. **Security Group**
   - Allows inbound SSH traffic (port 22)
   - Allows all outbound traffic

6. **EC2 Instance**
   - Instance Type: t2.micro
   - AMI: ami-06b21ccaeff8cd686
   - Auto-assigned public IP enabled

## Usage

1. **Clone/Create Configuration**
   ```bash
   # Create a new directory
   mkdir ec2-terraform
   cd ec2-terraform
   
   # Create main.tf file and paste the configuration
   ```

2. **Initialize Terraform**
   ```bash
   terraform init
   ```

3. **Review the Plan**
   ```bash
   terraform plan
   ```

4. **Apply the Configuration**
   ```bash
   terraform apply
   ```

5. **Destroy Resources (When Done)**
   ```bash
   terraform destroy
   ```

## Configuration Customization

To customize this configuration, you can modify the following variables in the `main.tf` file:

- `region`: Change AWS region (currently set to "us-east-1")
- `availability_zone`: Change availability zone (currently set to "us-east-1a")
- `instance_type`: Change EC2 instance type (currently set to "t2.micro")
- `ami`: Change the AMI ID based on your requirements
- `cidr_block`: Modify VPC or subnet CIDR ranges if needed

## Security Considerations

- The security group currently only allows SSH access (port 22)
- Consider adding additional security group rules for your specific use case
- It's recommended to restrict SSH access to specific IP ranges rather than 0.0.0.0/0

## Outputs

After successful creation, the template will output:
- Public IP address of the EC2 instance

## Important Notes

1. Ensure you have sufficient AWS permissions to create all resources
2. Resources created may incur costs in your AWS account
3. Always run `terraform destroy` when you're done to avoid unnecessary charges
4. The EC2 instance will be created without a key pair by default. Add a key pair configuration if SSH access is needed

## Troubleshooting

Common issues and solutions:

1. **AWS Credentials Not Found**
   - Run `aws configure` to set up your AWS credentials

2. **Resource Creation Failure**
   - Check if the AMI ID is valid for the us-east-1 region
   - Verify you have sufficient permissions in your AWS account
   - Ensure you're not hitting any AWS service limits

3. **Cannot Connect to Instance**
   - Verify security group rules
   - Ensure you have configured a key pair if needed
   - Check if the instance is running

## Contributing

Feel free to modify and improve this template based on your needs.
