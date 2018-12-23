package com.evento.apirest.resources;


import java.awt.image.BufferedImage;
import java.io.BufferedOutputStream;
import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.nio.charset.StandardCharsets;
import java.util.Base64;
import java.util.Calendar;
import java.util.Date;
import java.util.List;

import javax.imageio.ImageIO;
import javax.validation.Valid;
import javax.xml.bind.DatatypeConverter;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

import com.evento.apirest.models.Evento;
import com.evento.apirest.repository.EventoRepository;
import com.fasterxml.jackson.databind.deser.Deserializers.Base;

import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;

@CrossOrigin(origins = "*")
@RestController
@RequestMapping(value="/api")
@Api(value="API REST Evento")
public class EventoResource {
	
	@Autowired
	EventoRepository eventoRepository;
	
	@ApiOperation(value="Retorna uma lista de Eventos")
	@GetMapping("/eventos")
	public List<Evento> listaEventos(){
		return eventoRepository.findAll();
	}
	
	
	@GetMapping("/mensagem")
	public String mensagem(){
		return "API RESPONDENDO";
	}
	
	@ApiOperation(value="Retorna um evento unico")
	@GetMapping("/evento/{id}")
	public Evento listaEventoUnico(@PathVariable(value="id") long id){
		return eventoRepository.findById(id);
	}
	
	@ApiOperation(value="Salva um evento")
	@PostMapping("/evento/criar")
	public Evento salvaEvento(@RequestBody @Valid Evento evento) {
		
		
		String[] strings = evento.getImagem().split(",");
    	byte[] data = DatatypeConverter.parseBase64Binary(strings[1]);
    	
    	Date dataParAquivo = new Date();
    	Calendar cal = Calendar.getInstance();
    	
    	
    	
    	cal.setTime(dataParAquivo);
    	int dia = cal.get(Calendar.DAY_OF_MONTH);
    	int mes = cal.get(Calendar.MONTH);
    	int ano = cal.get(Calendar.YEAR);
    	int minutos = cal.get(Calendar.MINUTE);
    	int segundos = cal.get(Calendar.SECOND);
    	int milesegundos = cal.get(Calendar.MILLISECOND);
    	
    	
    	int nomeArquivo = dia*1+mes*2+ano*3+minutos*4+segundos*5+milesegundos*6;
    	
        String path = "C:\\Users\\Nicolas\\eclipse-workspace\\Imagens\\"+nomeArquivo+".png";
        File file = new File(path);
        try (OutputStream outputStream = new BufferedOutputStream(new FileOutputStream(file))) {
            outputStream.write(data);
        } catch (IOException e) {
            e.printStackTrace();
        }
        evento.setImagem(path);
        
		return eventoRepository.save(evento);
	}
	
	@ApiOperation(value="Deleta um evento")
	@DeleteMapping("/evento")
	public void deletaEvento(@RequestBody @Valid Evento evento) throws IOException {
		eventoRepository.delete(evento);
		
            

	}
	
	@ApiOperation(value="Atualiza um evento")
	@PutMapping("/evento")
	public Evento atualizaEvento(@RequestBody @Valid Evento evento) {
		return eventoRepository.save(evento);
	}
	 

}
