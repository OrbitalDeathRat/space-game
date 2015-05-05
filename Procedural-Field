using UnityEngine;
using System.Collections;
using System.Collections.Generic;

public class ProceduralField : MonoBehaviour {

	public int width;
	public int height;

	[Range(0, 100)]
	public int fillPercent;

	public string seed;
	public bool useRandomSeed;

	public GameObject asteroid;

	int[,] map;
	bool[,] tried;

	List<int[,]> mapList = new List<int[,]>();

	void Start(){
		GenerateMap ();
		for(int i = 0; i < 3; i++){
			SmoothMap ();
		}
		if (map != null) {
			tried = new bool[width,height];

			for(int x = 0; x < width; x++){
				for(int y = 0; y < height; y++) {
					if(map[x,y] == 1 && !tried[x,y]){
						int[,] mapChunk = new int[width, height];
						mapChunk = FloodFill(x, y, mapChunk);
						mapList.Add(mapChunk);
					}
				}
			}
			System.Random hrand = new System.Random(100);
			foreach(int[,] a in mapList){
				GameObject parent = new GameObject();
				parent.name = "Parent Container";
				int sizeCount = 0;
				List<Vector3> avgVecList = new List<Vector3>();
				for(int x = 0; x < width; x++){
					for(int y = 0; y < height; y++){
						if(a[x,y] == 1){
							avgVecList.Add(new Vector3(-width/2 + x +.5f, this.transform.position.y, -height/2 + y + .5f));
							sizeCount++;
						}
					}
				}
				Vector3 avgVec = Vector3.zero;
				foreach(Vector3 v in avgVecList){
					avgVec += v;
				}
				avgVec /= avgVecList.Count;
				avgVec.y = hrand.Next(-100, 100);
				GameObject g = Instantiate(asteroid, avgVec, Quaternion.identity) as GameObject;
				g.transform.parent = parent.transform;
				SphereCollider coll = g.GetComponent<SphereCollider>();
				if(sizeCount < 10){
					g.transform.localScale *= 3;
					coll.radius *= 3;
				}
				else if(sizeCount < 30){
					g.transform.localScale *= 5;
					coll.radius *= 5;
				}
				else if(sizeCount < 60){
					g.transform.localScale *= 10;
					coll.radius *= 10;
				}
				else {
					g.transform.localScale *= 15;
					coll.radius *= 15;
				}
			}
		}
	}

	void GenerateMap(){
		map = new int[width, height];
		RandomFillMap();
	}

	void SmoothMap(){
		for (int x = 0; x < width; x++) {
			for (int y = 0; y < height; y++) {
				int walls = GetWalls(x,y);
				if(walls < 3){
					map[x,y] = 0;
				}
				else if(walls > 3){
					map[x,y] = 1;
				}
			}
		}
	}

	int GetWalls(int arrX, int arrY){
		int wallCount = 0;
		for (int neighbourX = arrX - 1; neighbourX <= arrX + 1; neighbourX++) {
			for (int neighbourY = arrY -1; neighbourY <= arrY + 1; neighbourY++) {
				if(neighbourX >= 0 && neighbourX < width && neighbourY >= 0 && neighbourY < height){
					if (neighbourX != arrX || neighbourY != arrY) {
						wallCount+= map[neighbourX, neighbourY];
					}
				}
			}
		}
		return wallCount;
	}

	void RandomFillMap(){
		if(useRandomSeed){
			seed = Time.unscaledTime.ToString();
		}

		System.Random rand = new System.Random (seed.GetHashCode());

		for(int x = 0; x < width; x++){
			for(int y = 0; y < height; y++) {
				map[x,y] = (rand.Next(0,100) < fillPercent)? 1 : 0;
			}
		}

	}

	int[,] FloodFill (int x, int y, int[,] mapChunk){
		if (!tried [x, y]) {
			tried[x,y] = true;
		
			if(map[x,y] == 1){
				mapChunk[x,y] = map[x,y];
				//check left
				if (x-1 > 0) {
					FloodFill (x - 1, y, mapChunk);
				}
				//check up
				if (y-1 > 0) {
					FloodFill (x, y - 1, mapChunk);
				}

				//check right
				if (x + 1 < width) {
					FloodFill (x + 1, y, mapChunk);		
				}
				//check down
				if (y+1 < height) {
					FloodFill (x, y + 1, mapChunk);
				}
			}
		}
		return mapChunk;
	}
}
