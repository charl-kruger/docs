# Programmable Banking

Build your own rules and limits - Securely hosted Javascript functions that execute during your card transactions. Limit your fast-food spend, track your coffee intake on the fly - anything goes.

[![IMAGE ALT TEXT HERE](images/overview.gif)](https://www.youtube.com/watch?v=lO-fSgNOUkY)

## Prerequisite

This documentation assumes that you have a basic understanding of Javascript and, are aware of the consequences of executing programmatic logic against your card transactions, e.g. resulting in a transaction being decline as a result of logic you have programmed against your Investec card.

### Features included

- Online JS IDE/code editor based on Monaco Editor, the code editor that powers VS Code
- Two card transaction hooks with you can access with every card transaction, `beforeTransaction` and `afterTransaction`
- Intercept card transaction and decline based on your "code" with `beforeTransaction` hook
- Publish "code" to securely hosted VM instance
- Perform transaction simulation using online simulator
- Enable/disable the code executing against a specific card
- Access to the card authorization object and meta-data
- Run code after a processed using the afterTransaction() function. for instance: post your transaction to an app you built
- Call external an APIs using node-fetch

## main.js

`main.js` provides two methods required for the card transaction interception - `beforeTransaction` and `afterTransaction`. The `beforeTransaction` method has a limited window of 2 seconds to execute hence needs to be fast. `afterTransaction` has a much larger window limit of 15 seconds which gives you more time to communicate with internal and external resources.

### Before transaction

Every time you execute a transaction from your Investec card, the `beforeTransaction` method intercepts the authorization object before it is approved by Investec.

Within this method, you can apply logic to either **decline or approve** the transaction based on data from the card authorization itself, or via external data sources fetched via http. Please note that **you MUST return a boolean in order for this method to work**.

#### Approve authorization
```javascript
// main.js
const beforeTransaction = async (authorization) => {
    // always APPROVE
    return true;
}
```
`return true` will approve a authorization.

#### Decline authorization
```javascript
// main.js
const beforeTransaction = async (authorization) => {
    // always DECLINE
    return false;
}
```
`return false` will decline a authorization.

#### Apply conditional logic within before transaction method
```javascript
// main.js
const beforeTransaction = async (authorization) => {
    const fiftyRand = 5000; // authorization.amount is in cents

    if(authorization.centsAmount < fiftyRand) {
        return true
    } else {
        return false;
    }
}
```
Apply conditional logic within before transaction method
Say you wanted to decline any transaction that is R50.00 and above - if the authorization.centsAmount is less than R50.00, then approve. Else decline the transaction.

*TIP: Use console.log(authorization) to see available properties of the authorization that are accessible.*



![Drag Racing](images/mainjs_interface.png)

### Features
- Investec JS code editor (Monaco Editor backed, the code editor that powers VS Code) 
- Simulator
- Logs
- Access to Investec card transaction object

## Community
