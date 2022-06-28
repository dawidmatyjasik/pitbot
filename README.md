
# Dokumentacja
## addMessages
dodaje wiadomość, która ma zostać wyświetlona
```javascript
addMessages(prop){
  return [
    text: '' // tekst z ENUM
    params: {}, // zamienia z ENUM {{}} na propsy zmienne
    rollback: 1 //???
  ]
}
```
#### przykład: 
```javascript
addMessages(prop){
  return [
    text: 'stage_2.last_name' 
    params: {
                name: prop.name, 
              },
    rollback: 1 
  ]
}
```
## addActions
dodaje akcje na samym dole, które może wykonać użytkownik
```javascript 

//1
addActions() {
  return [
    actionButton({
      label: 'button.yes',
      style: ButtonStyleEnum.secondary,
      route: [STAGE.two, STAGE_2.spouse_birth_date_prompt],
  }),
    actionButton({
      label: 'button.no',
      style: ButtonStyleEnum.secondary,
      route: [STAGE.two, STAGE_2.spouse_birth_date_prompt],
  })

//2
addActions(){
  return [
    component: ActionComponentEnum.TextInput, //komponent jako enum
    name: validatorNamesEnum.first_name,
    placeholder: 'placeholders.spouse_first_name,
    onSubmit: () => {}
  ]
}


```

### onSubmit
metoda wykonywana w funkcji addActions() przy wysyłaniu formularza
```javascript 
const onSubmit = (prop) => {
            callAction();
          };

```


### callAction
Zapisuje, edytuje etc. w backendzie. Należy podać `ReducerEnum` oraz obiekt z danymi do wykonania działania
```javascript
callAction(ReducerEnum.profile.update, {
              data: { last_name },
              onSuccess: () => {
                setRoute(STAGE.two, STAGE_2.town_check);
              },
              onFail: () => {},

});
```



### setRoute
pozwala zmienić stage na kolejny
```javascript
setRoute(stageId, viewId)  // przechodzi do kolejnego widoku
```






### init
funkcja wywoływana na samym początku, która pozwala pobrać dane, a następnie je wykorzystać
```javascript
init() {
  const { postal_code } = getStoreState().profile.data;
   return await callAction(ReducerEnum.profile.fetch_towns, {
      data: { postal_code },
    });
}

```



### addMobileActions ???
chyba po prostu pod mobilne urządzenia - nie używamy
### addWebActions ???
