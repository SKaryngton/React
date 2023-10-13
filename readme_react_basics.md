- ### L'objet React et ReactDOM
```
-React permet de creer des elements HTML

-ReactDOM Permet d'inserer ces elements


// p est un paragraphe(p) sans attribut (null) et avec pour enfant le text (Mon Paragraphe 1)
var p =React.createElement('p',null,'Mon Paragraphe 1')

// p est inserer dans la div ayant pour id app
ReactDOM.render(p, document.getElementById('app'))

```
```
//creation d'un menu
//l'objet React ul est une liste(ul) avec pour attribut id (list) et avec pour enfants menu[] 

var menu = ['Accueil','Boutique','contact']

var ul = React.createElement('ul',{id:list},

//la propriete key est ajoute a fin de distinguer chaque elmt de la list
menu.map((elmt, index)=>{
    return React.createElement('li',{className:'list-item', key:'elmt-'+index}, elmt)
})
)

// insertion du menu
ReactDOM.render(ul, document.getElementById('app'))

```

-  ### L'objet Props (Read Only :accessible uniquement en lecture)

```
- l'objet Props est un objet contenant les attributs et les enfants de l'ojet react

var ul = React.createElement('ul',{id:list},

//la propriete key est ajoute a fin de distinguer chaque elmt de la list
menu.map((elmt, index)=>{
    return React.createElement('li',{className:'list-item', key:'elmt-'+index}, elmt)
})
)


ul.props = {id:"list", children:Array(3)}
ul.props.id="list"
ul.props.children[0].props={className:"list-item", children:"Accueil"}
```



- ### Les composants
    - sont des fonctions  reutilisables

          ```
          //la fonction reutilisatble listMenu est un composant 
          var listMenu = (props) =>{
              const menu = props.menu
          return React.createElement('ul',{id:'list'},
                                      menu.map((elmt, index)=>{
                                          return React.createElement('li',
                                              {className:'list-item', key:'elmt-'+index}, 
                                              elmt)
                                              })
                                      )
                              }
          //  Alternave vu l'on a pas besoin de tout les props  on peut juste recuperer menu
          var listMenu = ({menu}) =>{  
          return React.createElement('ul',{id:'list'},
                                      menu.map((elmt, index)=>{
                                          return React.createElement('li',
                                              {className:'list-item', key:'elmt-'+index}, 
                                              elmt)
                                              })
                                      )
                              }                

          //listmenu es ecrit sans () car on ne souhaite pas executer la fonction
          //De ce fait le parametre de la fonction es passe comme attribut
          var list = React.createElement(listMenu, {menu:['Accueil','Boutique','contact']})



          ReactDOM.render(list, document.getElementById('app'))
          ```  
    - sont des classes

          ```
            // la classe doit etendre la methode React.Component pour etre reconnu par React
              class listMenu extends React.Component{

                  constructor(props){
                      super(props)
                  }

                  // la methode render est obligatoire et retourne les elmts que l'on souhaite afficher
                  render(){
                  return  React.createElement('ul',{id:'list'},
                      this.props.menu.map((elmt, index)=>{
                      return React.createElement('li',
                          {className:'list-item', key:'elmt-'+index}, 
                          elmt)
                          })
                  )
                  }
              }

              var list = React.createElement(listMenu, {menu:['Accueil','Boutique','contact']})



              ReactDOM.render(list, document.getElementById('app'))     
          
          ```

- ### Le style

```
   return  React.createElement('ul',{id:'list'},
        this.props.menu.map((elmt, index)=>{
          return React.createElement('li',
              {
              className:'list-item', 
              style:{color:'red',backgroundColor:'black'},
              key:'elmt-'+index}, 
              elmt)
              })
       )
```

```
class listMenu extends React.Component{

    constructor(props){
        super(props)
    }

    // la methode render est obligatoire
    render(){
       return  React.createElement('ul',{id:'list'},
        this.props.menu.map((elmt, index)=>{
          return React.createElement('li',
              {
              className:'list-item', 
              style:this.props.style,
              key:'elmt-'+index}, 
              elmt)
              })
       )
    }
}

var list = React.createElement(listMenu, {menu:['Accueil','Boutique','contact'],style:{color:'red',background:'#ccc'}})



ReactDOM.render(list, document.getElementById('app'))     

```

- ### langage JSX extension de JS

```
permet d'ecrire un code plus lisible Pour les Humains

var index=2
var p= React.createElement('P',null,'Hello',index)   //JS
var P= <p> Hello {index} </p> //JSX


les clients ne comprennent que le HTML,CSS et le JS

On a besoin d'un compilateur qui compile le JSX en JS Pour le client
Babel est un excellent compilateur


<!DOCTYPE html>
<html lang="en">
<head>...</head>
<body>
    <div id="app">...</div>
    
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel" src="assets/js/main.js"></script>

</body>
</html>


```
```
// la classe doit etendre la methode React.Component pour etre reconnu par React
class listMenu extends React.Component{

    constructor(props){
        super(props)
    }

    // la methode render est obligatoire
    render(){
       return  <ul id='list'>
                   {
                    this.props.menu.map((elmt,index)=>{
                        return <li className='list-item' 
                        style={this.props.style} 
                        key={'elmt-'+ index}>

                        {elmt}
                        
                        </li>
                    })
                    }       
                </ul>
            }
}

var list = React.createElement(listMenu, {menu:['Accueil','Boutique','contact'],style:{color:'green',background:'#ccc'}})



ReactDOM.render(list, document.getElementById('app'))     

```