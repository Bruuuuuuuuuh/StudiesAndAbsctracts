  Data Transfer Object (DTO) or simply Transfer Object is a design
pattern widely used in Java to transport data between different
components of a system, different instances or processes of a 
distributed system or different systems via serialization. 

    Serialization: In general, serialization is a technique used to persist
    objects; basically: write objects to disk, transmit objects remotely over
    the network, store objects in a database and/or files (binary, xml, etc.) 
    
    You can often see *serialization errors*. It commonly ocurs when you are transmiting
    data to a server/database and acidentaly do a infinite loop, causing utterly 
    confusing and repetitive data output
  
  The idea is basically to group a set of attributes in a simple class
in order to optimize communication. In a remote call, it would be
inefficient to pass each attribute individually. It would likewise be 
inefficient or even cause errors to pass a more complex entity.


Examples of trasnmiting data to h2 without using dto:

Main method that gets the tecnico method:
    package com.pernalonga.helpdesk.resources;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    import com.pernalonga.helpdesk.domain.Tecnico;
    import com.pernalonga.helpdesk.domain.dtos.TecnicoDTO;
    import com.pernalonga.helpdesk.services.TecnicoService;

    @RestController
    @RequestMapping(value = "/tecnicos")
    public class TecnicoResource {
		
	//localhost:8080/tecnicos/1
	
	@Autowired
	private TecnicoService service;
	
	@GetMapping(value = "/{id}")
	public ResponseEntity<TecnicoDTO> findById(@PathVariable Integer id){
		//This method is a get to gets a tecnic by his Id
		
		Tecnico obj = service.findById(id);
		return ResponseEntity.ok().body(new TecnicoDTO(obj));
	
	}
}


Method Tecnic that gets and transfers data without dto:
    
    package com.pernalonga.helpdesk.domain;

    import java.util.ArrayList;
    import java.util.List;

    import javax.persistence.Entity;
    import javax.persistence.OneToMany;

    import com.fasterxml.jackson.annotation.JsonIgnore;
    import com.pernalonga.helpdesk.domain.enums.Perfil;


    @Entity
    public class Tecnico extends Pessoa{
      private static final long serialVersionUID = 1L;

	@JsonIgnore
	@OneToMany(mappedBy = "tecnico")
	List<Chamado> chamados = new ArrayList<>();
	
	public Tecnico() {
		super();
		addPerfil(Perfil.CLIENTE);
	}
	
	public Tecnico(Integer id, String nome, String cpf, String email, String senha) {
		super(id, nome, cpf, email, senha);
		addPerfil(Perfil.CLIENTE);
	}

	public List<Chamado> getChamados() {
		return chamados;
	}

	public void setChamados(List<Chamado> chamados) {
		this.chamados = chamados;
	    }
    }

Tecnic Method using dto:

    package com.pernalonga.helpdesk.domain.dtos;

    import java.time.LocalDate;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.stream.Collectors;

    import com.fasterxml.jackson.annotation.JsonFormat;
    import com.pernalonga.helpdesk.domain.Tecnico;
    import com.pernalonga.helpdesk.domain.enums.Perfil;

    public class TecnicoDTO {
    private static final long serialVersionUID = 1L;
	
	protected Integer id;
	protected String nome;
	protected String email;
	protected String cpf;
	protected String senha;
	
	protected Set<Integer> perfis = new HashSet<>();
	
	@JsonFormat(pattern = "dd/MM/yyyy")
	protected LocalDate dataCriacao = LocalDate.now();

	public TecnicoDTO() {
		super();

	}

	public TecnicoDTO(Tecnico obj) {
		super();
		this.id = obj.getId();
		this.nome = obj.getNome();
		this.cpf = obj.getCpf();
		this.email = obj.getEmail();
		this.senha = obj.getSenha();
		this.perfis = obj.getPerfis().stream().map(x -> x.getCodigo()).collect(Collectors.toSet());
		this.dataCriacao = obj.getDataCriacao();
	}

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getNome() {
		return nome;
	}

	public void setNome(String nome) {
		this.nome = nome;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public String getCpf() {
		return cpf;
	}

	public void setCpf(String cpf) {
		this.cpf = cpf;
	}

	public String getSenha() {
		return senha;
	}

	public void setSenha(String senha) {
		this.senha = senha;
	}

	public Set<Perfil> getPerfis() {
		return perfis.stream().map(x -> Perfil.toEnum(x)).collect(Collectors.toSet());
	}

	public void addPerfil(Perfil perfil) {
		this.perfis.add(perfil.getCodigo());
	}

	public LocalDate getDataCriacao() {
		return dataCriacao;
	}

	public void setDataCriacao(LocalDate dataCriacao) {
		this.dataCriacao = dataCriacao;
	  }
    } 
