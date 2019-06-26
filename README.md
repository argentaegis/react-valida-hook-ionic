React Valida Hook Ionic
==========================================
This is a fork of useful work done by Sergio Marin at react-valida-hook https://www.npmjs.com/package/react-valida-hook with minor modification so that it plays nice with React+Ionic.

All credit is to that team.

Custom hook to create validable forms using `valida-js` for validation

For validation rules see valida-js [docs](https://www.npmjs.com/package/valida-js)

**NOTE:**
Is important to know, valida-js don't return error message, only the and array of error types. Maybe will need to add a proper translation for those messages. That was made on porpuse in order to move translation to other place and not inside the validation library.

## How to install 

```bash
npm install react-valida-hook-ionic
```

## How to use it

```js
import React from 'react';
import {
  IonItem, IonInput, IonIcon, IonButton,
} from '@ionic/react';
import useValitedForm from 'react-valida-hook-ionic'

const initialState = {
  name: '',
  email: ''
}

const validations = [
  {
    name: 'name',
    type: 'required',
    stateMap: 'name'
  },
  {
    name: 'email',
    type: 'required',
    stateMap: 'email'
  },
  {
    name: 'email',
    type: 'isEmail',
    stateMap: 'email'
  }
]

function UserForm () {
  const [formData, validation, validateForm, getData] = useValitedForm(initialState, validations)
  const submit = (event) => {
    event.preventDefault()
    const valid = validateForm()
    console.log(getData())
  }
  return (
    <form noValidate={true} onSubmit={submit}>
      <IonItem>
        <IonIcon name={'mail'}/>
        <IonInput
          placeholder='Email'
          name='email'
          id='email'
          {...formData.email.input}
        />
        <div className='errors'>
          { validation.errors.email.join(', ')}
        </div>
      </IonItem>
      <IonItem>
        <IonIcon name={'person'}/>
        <IonInput
          placeholder='Display Name'
          name='name'
          id='name'
          {...formData.name.input}
        />
        <div className='errors'>
          { validation.errors.name.join(', ')}
        </div>
      </IonItem>
      <IonButton type='submit' expand='block'
      >
        JOIN THE SQUAD
      </IonButton>
    </form>
  )
}

export default UserForm;
```
