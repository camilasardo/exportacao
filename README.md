pragma solidity 0.5.12;

contract Exportacao { string public vendedor; string public comprador; uint256 public valor; uint256 public quantidade;

constructor(string memory nomeComprador, string memory nomeVendedor, uint256 valorDoAcucar, uint256 quantDeAcucar) public
{
    comprador = nomeComprador; 
    vendedor = nomeVendedor; 
    valor = valorDoAcucar;
    quantidade = quantDeAcucar;
}

function valorDoAcucar() public view returns (uint256) 
{
    return valor;
}

function quantDeAcucar() public view returns (uint256) 
{
    return quantidade;
}

    function valorAPagar(uint256 _valorDoAcucar, uint256 _quantDeAcucar) public view returns(uint256 valorTotalAPagar) 
{
    _valorDoAcucar = valor;
    _quantDeAcucar = quantidade;
    valorTotalAPagar = _valorDoAcucar*_quantDeAcucar;
    return valorTotalAPagar;
}
}   
