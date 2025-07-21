# Level Info
> Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:
>
> S1JZUFRPTklTR1JFQVQ=
> 
> Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/

All we need to get started is a base64 converter - you can use Powershell or Bash for this, but it's probably easier to use an online converter like [https://www.base64decode.org/](https://www.base64decode.org/).

Converting the string `S1JZUFRPTklTR1JFQVQ=` from base64 to plain ASCII we get our password for Level1: `KRYPTONISGREAT`
