# Lemon
ForLemon

//only the feb(10) at the moment
//

//console app side
using System;
using System.Net.Http;

namespace Lemon
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Feb(10) is");
            HttpClient client = new HttpClient();
            HttpResponseMessage response = client.GetAsync("https://localhost:5001/api/values/feb/10").Result;
            HttpContent content = response.Content;
            var result = content.ReadAsStringAsync();
            System.Threading.Thread.Sleep(2000);
            Console.WriteLine(result.Result);
        }
    }
}

//webservice side
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;

namespace WebService.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ValuesController : ControllerBase
    {
        [HttpGet("feb/{n}")]
        public int GetFeb(int n){
            if (n > 100 || n < 1) return -1;
            else return feb(n);
        }

        private int feb(int n){
            if (n == 1) return 1;
            if (n == 2) return 1;
            return feb(n - 1) + feb(n - 2);
        }
    }
}

