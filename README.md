import re
import sys

N = int(input())
text = sys.stdin.read()
comm_re = '<!--[\s\S]*?-->'
text = re.sub(comm_re, "", text)

content_re = r'<(\w+.*?)/?>'
contents = re.findall(content_re, text, re.DOTALL)

tag_re = r'(\w+) ?'
att_re = r'([\w\-]+)=\"([\s\S]*?)\"'

for con in contents:
    tag = re.finditer(tag_re, con)
    print(next(tag).group().strip())
    
    attrs = re.findall(att_re, con)
    
    for att in attrs:
        print(f'-> {att[0]} > {att[1]}')
