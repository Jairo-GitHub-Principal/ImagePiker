Selecionar imagem para exibição:

1 instalar biblioteca imgePicker

npm install react-native link 
npm install react-native-image-picker


pesquise tambem o uso do piker/piker no github

npm install @react-native-picker/picker --save 





//***********************************************************************************************************************************************************************

import React, { Component } from 'react';

import {
  
  ScrollView,
  Text,
  View,
  Button,Image
} from 'react-native';
import { launchCamera,launchImageLibrary } from 'react-native-image-picker';






class App extends Component{
  constructor(props) {
    super(props)
    this.state = {
       
      imageUser:"" // esse cada é onde vai ser armazenado a uri da  imagem, pra poder salvar em um DB, ou para queulquer outro tipo de uso
        
    }

}
  

 render(){
  const pickImageFromCamera = async () => {
    const options = {
      midiaType: 'photo',
      quality: 0.5,
      saveToPhotos: true, // ativa o salvamento na galeria de imagems, se colocar false o salvamento das fotos passa a ser no cache
      uri: '',
      type: '',
    }
    const result = await launchCamera(options);

    if (result.assets) {
      const img = result.assets[0].uri // pra pegar somente a uri
      console.log(JSON.stringify(img))
      this.setState({ imageUser: img })
    }
  }


  const pickImageFromGalery = async () => {

    const options = { midiaType: 'photo' };
    const result = await launchImageLibrary(options);

    if (result.assets) {

      const img = result.assets[0].uri // pra pegar somente a uri

      console.log(JSON.stringify(img))

      this.setState({ imageUser: img })
    }
  }
  

  return (
   
      <ScrollView>    
        <View>
          <Text> teste</Text>
          <View>
          <Button 
           title="imagem da galeria"
           onPress={() => pickImageFromGalery()} >
              
            </Button>

            <Button 
           title="imagem da camera"
           onPress={() => pickImageFromCamera()} >
              
            </Button>
            </View>
            
            {this.state.imageUser ? //  se imagem da camera foi capturada é verdadeiro, as caracteristicas de estilo em Image sera aplicada na imgem capturada para que ela seja exibida em uma previsualização na propria tela de cadastro e a mesma sera exibida antes de  salvar os dados
            <View style={{ borderWidth: 2, borderColor: 'white' }}>
              <Image style={{ marginVertical: 10, alignSelf: 'center', width:'90%', height: 250 }} source={{ uri: this.state.imageUser }} />

            </View>
            : // se não se a condição this.state.anuncio_image for falso, não havera alteração e continuara aparecendo o texto abaixo
            <Text style={{ textAlign: 'center', color: 'white', fontWeight: '700', margin: '2%', marginBottom: 50 }} >nenhuma imagem selecionada</Text>
          }


         
        </View>
      </ScrollView>
  );
 }
}



export default App;
