# -collection
#!/usr/bin/env python
# encoding: utf-8
import json
import urllib2
import re
def getdata(id):
'''Queries the Facebook API for the specific group ID, and populates the
results dictionary with the Group ID, User Name, and User ID'''
#An access token is now required for quering the group messages.
a_token='access_token=<access token>'
urlquery='https://graph.facebook.com/'+id+'/feed&limit=20?access_token='+ a_token +''
print urlquery
data=json.load(urllib2.urlopen(urlquery))
harvest = []
results = {}    
for item in data['data']:
    try:
        results = {}
        results['grpid'] = id
        user = item['from']
        results['uname'] = user['name']
        results['uid'] = user['id']
        harvest.append(results)
    except:
        pass

print len(harvest)
def getgrpids():
        urlquery='https://graph.facebook.com/<any username>'#can i put my app name?
                             #not clear from examples given on facebook graph api page.
        data=json.load(urllib2.urlopen(urlquery))
    ids=[]
    for item in data['data']:
    try:
        ids.append(item['id'])
    except:
        pass
return ids

def main():
    idres=getgrpids()
    for id in idres:
    #Loops through all of the group ids returned by getgrpids()
        print 'Group ID:', id 
        getdata(id) 

if __name__ == '__main__':
    main()
