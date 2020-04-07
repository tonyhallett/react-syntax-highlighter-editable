1) Supply initial code in props
2) Use the render prop, renderSH to render the syntax highlighter

Typing in the textarea will change the code for the rendered syntax highlighter.

```typescript
import * as React from "react";
export interface EditableRSHProps{
  renderSH:(code:string) => React.ReactNode,
  initialCode:string,
  rows:number,
  columns:number
}
export interface EditableRSHState{
  code:string
}

export class EditableRSH extends React.Component<EditableRSHProps,EditableRSHState>{
  constructor(props:EditableRSHProps){
    super(props);
    this.state = {code:props.initialCode}
  }
  codeChanged = (evt:any) => {
    this.setState({code:evt.target.value});
  }
  render(){
    return <div style={{display:'flex'}}>
      <textarea 
        style={{flex:'1 1 0%'}} 
        rows={this.props.rows} 
        cols={this.props.columns} 
        onChange={this.codeChanged} 
        value={this.state.code}/>
      <div style={{flex:'1 1 0%', width:'50%'}}>
      {this.props.renderSH(this.state.code)}
      </div>
    </div>
  }
}
```