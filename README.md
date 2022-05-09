<html>
<body leftmargin="0" marginwidth="0" topmargin="0" marginheight="0" offset="0" bgcolor='#FFFFFF' >
<STYLE>
 a { color:#FFFFFF;}
</STYLE>
<table width="550" cellpadding="20" cellspacing="0" bgcolor="#FFFFFF">
<tr>
<td bgcolor ="#FFFFFF" valign="top" style="font-size:12px;color:#000000;font-family:trebuchet ms;">

  {% if message %}
  <p style="font-weight:bold">{{message}}</p>
  {% endif %}

  <i style="color:#FF0000; font-size:12px">On {{ticket.last_comment.created_at | date_sw}}, {{ticket.last_comment.creator.full_name_or_email}} wrote:</i>
  {{ticket.last_comment.body | escape | simple_format}}
  <br/>
  {% if recipient.is_admin %}
    <div style="padding:8px; border:1px dotted #314D56; background-color: #9BBFCB; font-size:11px;">
      <h2 style="margin-bottom:5px; margin-top:0px; font-weight:bold; font-size:11px;">Ticket Overview</h2>
      Priority: {{ticket.priority | escape}}<br/>
      Creator: {{ticket.creator.full_name_or_email | escape}}<br/>
      Assignee: {{ticket.assignee.full_name_or_email | escape}}<br/>
      Ticket URL: <a href="{{ticket.url | escape}}">{{ticket.url | escape}}</a><br/>
          <br/>
         </div>
  {% endif %}

  {% if ticket.previous_comments != empty %}
    <br/>
    <h2 style="margin-bottom:1px; margin-top:1px; font-weight:bold; font-size:20px;">Ticket History</h2>
  {%endif%}

  {% for comment in ticket.previous_comments %}
    <div style="padding:8px; border:1px solid #CCCCCC; background-color: #EFEFEF; font-size:11px;">
    <i style="color:#555555; font-size:11px">On {{comment.created_at | date_sw}}, {{comment.creator.full_name_or_email | escape}} wrote:</i>
    {{comment.body | escape | simple_format}}
      {% endfor %}

  {% unless recipient.is_admin %}
    {% if ticket.previous_comments == empty %}<hr/>{% endif %}
    This is an automated response.  Your issue has been noted.  We'll be in touch soon.<br/>
    If you want to add more information about this problem, simply reply to this email.
    <br/>

</a><br/>
  {% endunless %}
</td>
</tr>
</table>
</body>
</html>
