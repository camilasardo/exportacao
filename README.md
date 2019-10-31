pragma solidity 0.5.12;

contract Exportacao {
        string public vendedor; 
        string public comprador;
        string public transportador;
        uint256 private valor; 
        uint256 private quantidade;
        address payable public contaVendedor;
        address public contaComprador;
        address public contaTransportador;
        bool public acucarEntregue;
        bool public exportPago;
    
    event exportacaoConcluida (uint256 quantidade);
    
    constructor(string memory nomeComprador, string memory nomeVendedor, string memory nomeTransportador, uint256 valorDoAcucar, uint256 quantDeAcucar, address payable _contaVendedor, address _contaComprador, address _contaTransportador) public {
        comprador = nomeComprador; 
        vendedor = nomeVendedor;
        transportador = nomeTransportador;
        valor = valorDoAcucar; 
        quantidade = quantDeAcucar;
        contaVendedor = _contaVendedor;
        contaComprador = _contaComprador;
        contaTransportador = _contaTransportador;
    }

    function valorDoAcucar() public view returns (uint256) { 
        return valor; 
    }

    function quantDeAcucar() public view returns (uint256) { 
        return quantidade; 
    }

    function valorAPagar() public view returns(uint256 valorTotalAPagar) { 
        valorTotalAPagar = valor*quantidade; 
        return valorTotalAPagar; 
    }

    function registroEntrega() public {
        require (msg.sender == contaTransportador, "Apenas transportador");
        acucarEntregue = true;
    }
    
    function pagamento () public payable {
        require (msg.value == valorAPagar());
        require (acucarEntregue == true);
        contaVendedor.transfer (msg.value); 
        exportPago = true;
        emit exportacaoConcluida (quantidade);
    }
}
