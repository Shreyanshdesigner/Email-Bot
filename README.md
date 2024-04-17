import pandas as p
import smtplib as sm



from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText


data = p.read_excel("students.xlsx")
# print(type(data))
# print(data._str_())
email_col = data.get("email")
list_of_emails = list(email_col)
print(list_of_emails)

try:
    server = sm.SMTP("smtp.gmail.com", 587)
    server.starttls()
    server.login("avinshverma9504@gmail.com", 'kvev muii krok iddm')
    from_ = "avinashverma9504@gmail.com"
    to_ = list_of_emails
    message = MIMEMultipart("alternative")
    message['subject'] = "This is just testing message"
    message["from"] = "avinashverma9504@gmail.com"

    html = '''
    <html>
    <head>

    </head>
    <body>
        <h1>This is shreyansh verma</h1>
        <h2>i just want to say hii</h2>
        <p>this id for testing</p>
        <button style="padding:20px;background:green;color:white">varify</button>

    </body>

    </html>


    '''

    part2 = MIMEText(html, "html")

    message.attach(part2)
    server.sendmail(from_, to_, message.as_string())
    print("message has been to the emails")



except Exception as e:
      print(e)
